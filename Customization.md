# How to Add Product Customization Controls to Any Widget
## Super Beginner-Friendly Guide (5-Year-Old Level!)

This guide will teach you how to add the 6 product customization controls to any product widget, step by step!

---

## 🎯 What You'll Add

You'll add **6 toggle switches** that let users control:
1. Show Quick View button
2. Show Compare button  
3. Show Wishlist button
4. Show Add to Cart button
5. Enable Hover Image (2nd image on mouse hover)
6. Enable Animations (fancy hover effects)

---

## 📋 Before You Start

**You need to add code in TWO places:**
1. **Place A**: Add the toggle controls (buttons in Elementor editor)
2. **Place B**: Add the settings to loop_settings (makes controls actually work)

---

## 🔍 STEP 1: Find the Right File

1. Go to your theme folder:
   ```
   wp-content/themes/minimog/elementor/widgets/woocommerce/
   ```

2. Find the product widget file you want to edit. **These are the EXACT files that can have these controls:**
   - `product-carousel.php` (Product Carousel widget)
   - `product.php` (Products grid/list widget)
   - `product-grid-tabs.php` (Product Grid with Tabs widget)
   - `product-carousel-countdown.php` (Product Carousel with Countdown widget)
   - `product-carousel-tabs.php` (Product Carousel with Tabs widget)
   - `products-slideshow.php` (Products Slideshow widget)

3. **Pick ONE file** from the list above that you want to add controls to

4. Open that file in your code editor

---

## ⚠️ IMPORTANT: Which Files to SKIP

**DO NOT add these controls to these files:**
- `product-list-carousel.php` (this one doesn't need these controls)
- Any file with "category" in the name like `product-categories-grid.php` (they show categories, not products)
- Any file with "brand" in the name like `product-brands.php` (they show brands, not products)

**ONLY use the 6 files listed in Step 1 above!**

---

## 🔍 STEP 2: Find PLACE A (Where to Add Controls)

### What to Look For:

Search for a line that says:
```php
$this->add_control( 'show_stock_bar', [
```

This is usually around line **120-200** depending on the widget.

### What It Looks Like:

You'll see something like this:
```php
$this->add_control( 'show_stock_bar', [
    'label'        => __( 'Show Stock Bar', 'minimog' ),
    'type'         => Controls_Manager::SWITCHER,
    'return_value' => '1',
] );
```

### 👀 Important: Find Where It ENDS

Look for the **closing bracket and semicolon** ⬇️
```php
] );    ← This line ends the 'show_stock_bar' control
```

**The next control usually starts right after** with something like:
```php
$this->add_control( 'thumbnail_default_size', [
```

---

## ✏️ STEP 3: Add the Controls (PLACE A)

**AFTER** the `show_stock_bar` control ends (after the `] );` line), **BEFORE** the next control starts, **paste this ENTIRE block**:

```php

$this->add_control( 'product_actions_heading', [
	'label'     => __( 'Product Actions', 'minimog' ),
	'type'      => Controls_Manager::HEADING,
	'separator' => 'before',
] );

$this->add_control( 'show_quick_view', [
	'label'        => __( 'Show Quick View', 'minimog' ),
	'type'         => Controls_Manager::SWITCHER,
	'return_value' => '1',
	'default'      => '1',
] );

$this->add_control( 'show_compare', [
	'label'        => __( 'Show Compare', 'minimog' ),
	'type'         => Controls_Manager::SWITCHER,
	'return_value' => '1',
	'default'      => '1',
] );

$this->add_control( 'show_wishlist', [
	'label'        => __( 'Show Wishlist', 'minimog' ),
	'type'         => Controls_Manager::SWITCHER,
	'return_value' => '1',
	'default'      => '1',
] );

$this->add_control( 'show_add_to_cart', [
	'label'        => __( 'Show Add to Cart', 'minimog' ),
	'type'         => Controls_Manager::SWITCHER,
	'return_value' => '1',
	'default'      => '1',
] );

$this->add_control( 'product_display_heading', [
	'label'     => __( 'Product Display', 'minimog' ),
	'type'      => Controls_Manager::HEADING,
	'separator' => 'before',
] );

$this->add_control( 'enable_hover_image', [
	'label'        => __( 'Enable Hover Image', 'minimog' ),
	'description'  => __( 'Show 2nd product image on hover', 'minimog' ),
	'type'         => Controls_Manager::SWITCHER,
	'return_value' => '1',
	'default'      => '1',
] );

$this->add_control( 'enable_animations', [
	'label'        => __( 'Enable Animations', 'minimog' ),
	'description'  => __( 'Enable hover animations and transitions', 'minimog' ),
	'type'         => Controls_Manager::SWITCHER,
	'return_value' => '1',
	'default'      => '1',
] );

```

### 📸 Visual Guide:

**BEFORE** (what you see):
```php
$this->add_control( 'show_stock_bar', [
    'label'        => __( 'Show Stock Bar', 'minimog' ),
    'type'         => Controls_Manager::SWITCHER,
    'return_value' => '1',
] );                                          ← Control ends here

$this->add_control( 'thumbnail_default_size', [  ← Next control starts
```

**AFTER** (what it should look like):
```php
$this->add_control( 'show_stock_bar', [
    'label'        => __( 'Show Stock Bar', 'minimog' ),
    'type'         => Controls_Manager::SWITCHER,
    'return_value' => '1',
] );                                          ← Control ends here

$this->add_control( 'product_actions_heading', [  ← NEW! You added this
    'label'     => __( 'Product Actions', 'minimog' ),
    'type'      => Controls_Manager::HEADING,
    'separator' => 'before',
] );

$this->add_control( 'show_quick_view', [       ← NEW! You added this
    'label'        => __( 'Show Quick View', 'minimog' ),
    'type'         => Controls_Manager::SWITCHER,
    'return_value' => '1',
    'default'      => '1',
] );

... (rest of the new controls) ...

$this->add_control( 'thumbnail_default_size', [  ← Original next control
```

---

## 🔍 STEP 4: Find PLACE B (Where to Add Settings)

### What to Look For:

Search for:
```php
$this->loop_settings = [
```

OR sometimes it's just:
```php
$loop_settings = [
```

This is usually around line **40-80** or sometimes **700-1000** depending on the widget.

### What It Looks Like:

You'll see something like this:
```php
$this->loop_settings = [
    'layout'            => 'slider',
    'style'             => $style,
    'caption_style'     => $caption_style,
    'show_price'        => ! empty( $settings['show_price'] ) ? 1 : 0,
    'show_variation'    => ! empty( $settings['show_variation'] ) ? 1 : 0,
    'show_category'     => ! empty( $settings['show_category'] ) ? 1 : 0,
    'show_brand'        => ! empty( $settings['show_brand'] ) ? 1 : 0,
    'show_rating'       => ! empty( $settings['show_rating'] ) ? 1 : 0,
    'show_availability' => ! empty( $settings['show_availability'] ) ? 1 : 0,
    'show_stock_bar'    => ! empty( $settings['show_stock_bar'] ) ? 1 : 0,
];
```

### 👀 Important: Find the LAST Setting Line

Look for the **very last line before the closing `];`**

In the example above, it's:
```php
'show_stock_bar'    => ! empty( $settings['show_stock_bar'] ) ? 1 : 0,
                                                                       ↑
                                                    Notice the comma here!
```

---

## ✏️ STEP 5: Add the Settings (PLACE B)

**AFTER** the last setting line (like `'show_stock_bar'...`), **BEFORE** the closing `];`, **add these 6 lines**:

```php
'show_quick_view'   => ! empty( $settings['show_quick_view'] ) ? 1 : 0,
'show_compare'      => ! empty( $settings['show_compare'] ) ? 1 : 0,
'show_wishlist'     => ! empty( $settings['show_wishlist'] ) ? 1 : 0,
'show_add_to_cart'  => ! empty( $settings['show_add_to_cart'] ) ? 1 : 0,
'enable_hover_image' => ! empty( $settings['enable_hover_image'] ) ? 1 : 0,
'enable_animations'  => ! empty( $settings['enable_animations'] ) ? 1 : 0,
```

### 📸 Visual Guide:

**BEFORE**:
```php
$this->loop_settings = [
    'style'             => $style,
    'caption_style'     => $caption_style,
    'show_price'        => ! empty( $settings['show_price'] ) ? 1 : 0,
    'show_stock_bar'    => ! empty( $settings['show_stock_bar'] ) ? 1 : 0,
];                      ← Array closes here
```

**AFTER**:
```php
$this->loop_settings = [
    'style'             => $style,
    'caption_style'     => $caption_style,
    'show_price'        => ! empty( $settings['show_price'] ) ? 1 : 0,
    'show_stock_bar'    => ! empty( $settings['show_stock_bar'] ) ? 1 : 0,
    'show_quick_view'   => ! empty( $settings['show_quick_view'] ) ? 1 : 0,    ← NEW!
    'show_compare'      => ! empty( $settings['show_compare'] ) ? 1 : 0,       ← NEW!
    'show_wishlist'     => ! empty( $settings['show_wishlist'] ) ? 1 : 0,      ← NEW!
    'show_add_to_cart'  => ! empty( $settings['show_add_to_cart'] ) ? 1 : 0,  ← NEW!
    'enable_hover_image' => ! empty( $settings['enable_hover_image'] ) ? 1 : 0, ← NEW!
    'enable_animations'  => ! empty( $settings['enable_animations'] ) ? 1 : 0, ← NEW!
];                      ← Array closes here
```

---

## ⚠️ IMPORTANT RULES

### Rule 1: Watch Your Commas!
- Every line EXCEPT the last one needs a comma `,` at the end
- The last line before `];` should also have a comma

✅ **CORRECT**:
```php
'show_stock_bar'    => ! empty( $settings['show_stock_bar'] ) ? 1 : 0,    ← Has comma
'show_quick_view'   => ! empty( $settings['show_quick_view'] ) ? 1 : 0,   ← Has comma
'enable_animations'  => ! empty( $settings['enable_animations'] ) ? 1 : 0, ← Has comma
];
```

❌ **WRONG**:
```php
'show_stock_bar'    => ! empty( $settings['show_stock_bar'] ) ? 1 : 0    ← Missing comma!
'show_quick_view'   => ! empty( $settings['show_quick_view'] ) ? 1 : 0,
];
```

### Rule 2: Copy EXACTLY!
- Don't change `$this->` to `$`
- Don't change spacing or tabs
- Copy the entire block exactly as shown

### Rule 3: Keep Indentation!
- If the existing lines have tabs or spaces at the start, your new lines should too
- Make your new lines match the same indentation as the lines around them

---

## 🎯 Quick Checklist

Before you save the file, check these:

- [ ] Did you add the controls AFTER `show_stock_bar` ends?
- [ ] Did you add the controls BEFORE the next control starts?
- [ ] Did you add all 6 settings lines to `loop_settings`?
- [ ] Did you add them BEFORE the closing `];`?
- [ ] Does every line have a comma at the end?
- [ ] Did you keep the same indentation (tabs/spaces)?
- [ ] Did you save the file?

---

## 🧪 How to Test

1. **Clear WordPress cache** (if you have a caching plugin)
2. **Go to Elementor** editor
3. **Add or edit** the widget you modified
4. **Look for** two new sections in the Layout tab:
   - "Product Actions" (with 4 toggles)
   - "Product Display" (with 2 toggles)
5. **Toggle them ON/OFF** and preview!

---

## 🆘 Common Mistakes & Fixes

### Error: "Parse error" or "Syntax error"
**Cause:** Missing comma or bracket  
**Fix:** Check that all lines end with commas and brackets match `[` with `]`

### Error: Controls don't appear in Elementor
**Cause:** Added in wrong location  
**Fix:** Make sure you added AFTER `show_stock_bar` and within the `add_layout_section()` function

### Error: Toggles don't do anything
**Cause:** Didn't add to `loop_settings`  
**Fix:** Make sure you completed BOTH Place A and Place B

### Error: White screen
**Cause:** PHP syntax error  
**Fix:** Revert the file using FTP/File Manager, then try again carefully

---

## 📝 Real Example (product-carousel.php)

Here's exactly what I did to `product-carousel.php`:

### PLACE A: Lines 141-201
**Found:** Line 141 had `$this->add_control( 'show_stock_bar', [`  
**Action:** After line 145 where it closed with `] );`, I added the entire block of 6 controls  
**Result:** Controls now show in Elementor!

### PLACE B: Lines 42-58
**Found:** Line 42 had `$this->loop_settings = [`  
**Action:** After line 51 which had `'show_stock_bar'`, I added 6 new lines  
**Result:** Controls now actually work!

---

## 🎓 You're Done!

You now know how to add these controls to ANY product widget! Just follow the same steps:

1. Find `show_stock_bar` control
2. Add the 6 controls after it
3. Find `loop_settings` array
4. Add the 6 settings lines
5. Save and test!

**Pro Tip:** Always make a backup of the file before editing! 🔐
