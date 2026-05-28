When I ask to create a custom Shopify section with slider, always use my custom Swiper slider format.

Do not use Shopify native slider. Always use Swiper.

Follow this structure:

## 1. Add section CSS file at top:
{{ 'section-name.css' | asset_url | stylesheet_tag }}

## 2. Use my spacing style structure:
- Desktop padding/margin applied from 750px media query using `#shopify-section-{{ section.id }}` for margin and `.section-{{ section.id }}-padding` for padding.
- Mobile padding uses `padding_top_mobi` and `padding_bottom_mobi` schema settings.
- Do NOT calculate mobile margin from desktop values. Only desktop margin is used (inside the min-width: 750px block). Mobile has no margin override unless specifically requested.

## 3. Always create slider options using capture:

IMPORTANT: Do not add a trailing comma after the last object inside the capture block.
Use Liquid `unless forloop.last` or carefully order conditions to avoid trailing commas,
because trailing commas in JSON will cause JavaScript parse errors.

{%- capture slider_options -%}
  "slidesPerView": 3,
  "spaceBetween": 20,
  "loop": true
  {% if section.settings.show_pagination %}
  ,"pagination": {
    "el": "#shopify-section-{{ section.id }} .swiper-pagination",
    "clickable": true
  }
  {% endif %}
  ,"autoplay": {
    "delay": 3000,
    "disableOnInteraction": false
  }
  {% if section.settings.navigation %}
  ,"navigation": {
    "nextEl": "#shopify-section-{{ section.id }} .swiper-button-next",
    "prevEl": "#shopify-section-{{ section.id }} .swiper-button-prev"
  }
  {% endif %}
  ,"breakpoints": {
    "0": {
      "slidesPerView": 1,
      "spaceBetween": 15
    },
    "749": {
      "slidesPerView": 2,
      "spaceBetween": 20
    },
    "990": {
      "slidesPerView": {% if section.settings.auto_width %}"auto"{% else %}3{% endif %},
      "spaceBetween": 40
    },
    "1400": {
      "slidesPerView": {% if section.settings.auto_width %}"auto"{% else %}4{% endif %},
      "spaceBetween": {{ section.settings.space_between_slide }}
    }
  }
{%- endcapture -%}

## 4. Use this main section wrapper:

<div class="section-{{ section.id }} section-{{ section.id }}-padding section-{{ section.id }}-margin color-{{ section.settings.color_scheme }} gradient section-main-box CUSTOM-SECTION-CLASS">
  <div class="page-width">
    Section content here
  </div>
</div>

## 5. If slider is enabled, use this structure:

{% if section.settings.enable_slider %}
  <div class="swiper-main-wrapper">
    <div class="swiper" data-slider-options='{ {{ slider_options }} }'>
      <div class="swiper-wrapper">
        {% for block in section.blocks %}
          <div class="swiper-slide{% if section.settings.auto_width %} auto-width{% endif %}">
            Block content here
          </div>
        {% endfor %}
      </div>
    </div>

    {% if section.settings.navigation %}
      <div class="nav-btns {% if section.settings.show_navigation_in == 'desktop' %}small-hide{% endif %}{% if section.settings.show_navigation_in == 'mobile' %} medium-hide large-up-hide{% endif %}">
        <div class="btn-arrow swiper-button-prev" aria-label="Previous slide">{{ 'left-arrow.svg' | inline_asset_content }}</div>
        <div class="btn-arrow swiper-button-next" aria-label="Next slide">{{ 'right-arrow.svg' | inline_asset_content }}</div>
      </div>
    {% endif %}

    {% if section.settings.show_pagination %}
      <div class="swiper-pagination {{ section.settings.pagination_type }}{% if section.settings.show_pagination_in == 'desktop' %} small-hide{% endif %}{% if section.settings.show_pagination_in == 'mobile' %} medium-hide large-up-hide{% endif %}" aria-hidden="true"></div>
    {% endif %}
  </div>

## 6. If slider is disabled, always create normal grid/list fallback:

{% else %}
  <div class="section-name-items">
    {% for block in section.blocks %}
      <div class="section-name-item">
        Block content here
      </div>
    {% endfor %}
  </div>
{% endif %}

## 7. Always include these slider schema settings:

{
  "type": "header",
  "content": "Slider Options"
},
{
  "type": "checkbox",
  "id": "enable_slider",
  "default": false,
  "label": "Enable Slider"
},
{
  "type": "checkbox",
  "id": "auto_width",
  "default": false,
  "label": "Auto width"
},
{
  "type": "range",
  "id": "space_between_slide",
  "min": 0,
  "max": 200,
  "step": 2,
  "unit": "px",
  "label": "Space Between Slide",
  "default": 40
},
{
  "type": "checkbox",
  "id": "show_pagination",
  "default": false,
  "label": "Show pagination"
},
{
  "type": "select",
  "id": "show_pagination_in",
  "options": [
    {
      "value": "both",
      "label": "Both"
    },
    {
      "value": "desktop",
      "label": "Desktop"
    },
    {
      "value": "mobile",
      "label": "Mobile"
    }
  ],
  "default": "both",
  "label": "Show pagination in"
},
{
  "type": "select",
  "id": "pagination_type",
  "options": [
    {
      "value": "dot",
      "label": "Dot"
    },
    {
      "value": "border",
      "label": "Dot border"
    },
    {
      "value": "line",
      "label": "Line"
    },
    {
      "value": "number",
      "label": "Number"
    }
  ],
  "default": "dot",
  "label": "Pagination type"
},
{
  "type": "checkbox",
  "id": "navigation",
  "label": "Show navigation",
  "default": true
},
{
  "type": "select",
  "id": "show_navigation_in",
  "options": [
    {
      "value": "both",
      "label": "Both"
    },
    {
      "value": "desktop",
      "label": "Desktop"
    },
    {
      "value": "mobile",
      "label": "Mobile"
    }
  ],
  "default": "both",
  "label": "Show navigation in"
}

## 8. Always rename everything based on the new section:
- CSS file name
- schema name
- schema class
- wrapper class
- item class
- block type
- preset name

## 9. Do not copy `icon-with-text` names unless I ask for icon with text section.

## 10. CSS must be separate and one-line per selector. If multiple responsive CSS rules use the same media breakpoint, group them inside one media query block and keep each selector one line inside that shared block.

## 11. Do NOT add JavaScript in the section file.

Swiper is already globally initialized in `theme-vendors.js`.
It automatically finds every `.swiper[data-slider-options]` element on the page and initializes it.

- Do NOT write any `<script>` tag or JS block in the section.
- Do NOT manually call `new Swiper(...)` in the section.
- The section only needs the correct HTML structure with `data-slider-options` attribute on the `.swiper` element.
- `theme-vendors.js` handles initialization, multiple instances, and all Swiper options automatically.

## 12. Always create clean Shopify Dawn-compatible code.

## 13. Shopify schema JSON must always be formatted as expanded multi-line JSON objects. Do not write schema settings, blocks, presets, or options as one-line objects.

## 14. When creating section headings/titles for custom sections:

* Always follow my predefined section heading structure.
* Use dynamic alignment settings.
* Keep Dawn animation compatibility.
* Use conditional checks properly.
* Reuse this exact structure unless I request a different layout.

IMPORTANT: The heading condition checks for `section.settings.heading` and `section.settings.sec_text`.
Do NOT use `sub_title` in the condition — the correct id is `sec_text`.

```liquid
{% if section.settings.heading != blank or section.settings.sec_text != blank %}
  <div class="sec-head text-align-{{ section.settings.text_align }}{% if settings.animations_reveal_on_scroll %} scroll-trigger animate--slide-in{% endif %}">

    {% if section.settings.heading != blank %}
      <h2 class="sec-title">{{ section.settings.heading }}</h2>
    {% endif %}

    {% if section.settings.sec_text != blank %}
      <div class="sec-text">{{ section.settings.sec_text }}</div>
    {% endif %}

  </div>
{% endif %}
```

* Use `inline_richtext` for headings/subheadings when appropriate.
* Use `richtext` for description content (`sec_text`).
* Always include matching schema settings.
* Keep heading structure reusable and Dawn-compatible.
* Ensure structure works properly for multiple section instances.

Schema example:

```json
{
  "type": "inline_richtext",
  "id": "heading",
  "label": "Heading",
  "default": "Section heading"
},
{
  "type": "richtext",
  "id": "sec_text",
  "label": "Content",
  "default": "<p>Add section content here</p>"
},
{
  "type": "select",
  "id": "text_align",
  "label": "Text alignment",
  "default": "center",
  "options": [
    {
      "value": "left",
      "label": "Left"
    },
    {
      "value": "center",
      "label": "Center"
    },
    {
      "value": "right",
      "label": "Right"
    }
  ]
}
```


When I say "custom section with slider", automatically follow this format.
