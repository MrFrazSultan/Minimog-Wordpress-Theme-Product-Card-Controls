# 🧸 Simple Guide to Fixing Elementor Templates

If you update your theme, these special "fixes" might disappear! Here is how to put them back, even if you are not a computer expert.

### 🌟 What are we doing?
We are putting a "Magic Box" around the theme's old designs. If you have an Elementor design ready, the box says: *"Use the Elementor design!"* If not, it says: *"Use the old theme design."*

The "Magic Box" has two parts:
1.  **The Start Tag:** `<?php if ( ! minimog_has_elementor_template( 'archive' ) ) : ?>`
2.  **The End Tag:** `<?php endif; ?>`

---

## 📂 1. Shop & Category Pages
**File:** `woocommerce/archive-product.php`

**How to fix it:**
1.  Look for line **24**: `<div id="page-content" class="page-content">`
2.  **Right BELOW** that line, paste the **Start Tag**:
    ```php
    <?php if ( ! minimog_has_elementor_template( 'archive' ) ) : ?>
    ```
3.  Scroll all the way to the bottom. Look for line **128**: `</div>` (just before the last bit of code).
4.  **Right ABOVE** that line, paste the **End Tag**:
    ```php
    <?php endif; ?>
    ```

---

## 📂 2. Single Product Page
**File:** `woocommerce/single-product.php`

**How to fix it:**
1.  Look for line **25**: `<div id="page-content" class="page-content">`
2.  **Right BELOW** that line, paste the **Start Tag**:
    ```php
    <?php if ( ! minimog_has_elementor_template( 'single' ) ) : ?>
    ```
3.  Look for line **45**: `<?php do_action( 'woocommerce_after_single_product' ); ?>`
4.  **Right ABOVE** that line, paste the **End Tag**:
    ```php
    <?php endif; ?>
    ```

---

## 📂 3. The Search Page
**File:** `search.php`

**How to fix it:**
1.  Look for line **13**: `<div class="container">`
2.  **Right BELOW** that line, paste the **Start Tag**:
    ```php
    <?php if ( ! minimog_has_elementor_template( 'archive' ) ) : ?>
    ```
3.  Look for the **SECOND to last** `</div>` at the bottom (around line **41**).
4.  **Right ABOVE** that line, paste the **End Tag**:
    ```php
    <?php endif; ?>
    ```

---

## 📂 4. The 404 (Not Found) Page
**File:** `404.php`

**How to fix it:**
1.  Look for line **18**: `<div class="page-404-content">`
2.  **Right ABOVE** that line, paste the **Start Tag**:
    ```php
    <?php if ( ! minimog_has_elementor_template( 'single' ) ) : ?>
    ```
3.  Look for line **69**: `</div>` (the last one).
4.  **Right BELOW** that line, paste the **End Tag**:
    ```php
    <?php endif; ?>
    ```

---

## 📂 5. Cart & Checkout Pages
**Files:** `woocommerce/cart/cart.php` and `woocommerce/checkout/form-checkout.php`

**The Rule:**
Wrap the main "content" box inside these files with this tag:
```php
<?php if ( ! minimog_has_elementor_template( 'archive' ) && ! minimog_has_elementor_template( 'single' ) ) : ?>
... (the old code stays inside) ...
<?php endif; ?>
```

---

### ⚠️ Important Rules:
*   **Don't touch anything else!** Just add the tags at the start and end of the big "boxes."
*   **Look for `<div id="page-content"...>`**: This is usually the start of the box we want to wrap.
*   **Save your work!** Always keep a copy of your files before you change them.
