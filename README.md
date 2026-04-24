**Document Type:** Application / Website Overview (for QA Documentation)
**Application Name:** Sauce Demo Store
**URL (Base):** https://sauce-demo.myshopify.com/
**Platform:** Shopify ( Sandbox Store)
**Document Version:** 1.0
**Date:** 2026-01
**Author:** Kamogelo And other QA teams

---

## 1. Purpose of this Document

This document provides a **complete functional and structural overview** of the Sauce Demo Shopify storefront. It is intended to serve as the **baseline reference** for all QA activities including:

- Manual test case design
- Test scenario identification
- Defect reporting
- Regression planning
- Automation scripting (Selenium / Playwright / Cypress)

All subsequent test case manuals will be built on top of this overview.

---

## 2. Application Summary

| Attribute | Value |
|-----------|-------|
| **Application Type** | E-commerce website (B2C) |
| **Platform / CMS** | Shopify |
| **Industry** | Apparel & Accessories (Fashion) |
| **Target Audience** | Online shoppers looking for clothing, shoes, and accessories |
| **Primary Currency** | GBP (£) |
| **Primary Language** | English |
| **Accessibility** | Public — no login required to browse |
| **Checkout** | Shopify standard checkout (guest + registered) |
| **Authentication** | Email & Password + \"Shop\" social login |
| **Mobile Friendly** | Yes — responsive theme |

---

## 3. Site Map & Page Inventory

```
Sauce Demo Store (/)
│
├── Home (/)
│   └── Featured products (3)
│
├── Products / Collections
│   ├── All Products         → /collections/all
│   ├── Frontpage Collection → /collections/frontpage
│   └── Product Detail Page  → /products/{product-handle}
│                              → /collections/all/products/{product-handle}
│
├── Search
│   └── Search Results       → /search?q={query}
│
├── Cart
│   └── Shopping Cart        → /cart
│
├── Account
│   ├── Login                → /account/login
│   ├── Register             → /account/register
│   └── Forgot Password      → (inline toggle on /account/login)
│
└── Checkout (Shopify-hosted)
    ├── Contact / Shipping
    ├── Shipping Method
    ├── Payment
    └── Order Confirmation
```

---

## 4. Page-by-Page Breakdown

### 4.1 Home Page (`/`)

**Purpose:** Landing page — showcases featured products and store branding.

| Element | Description |
|---------|-------------|
| Header | Store name/logo, navigation, cart icon (count badge), account link |
| Featured Products | 3 products on homepage (Grey jacket, Noir jacket, Striped top) |
| Product Card | Image, Title, Price, clickable link to product detail |
| Cart Indicator | \"Your cart is empty.\" or count summary |
| Footer | Links, copyright, payment icons (Shopify default) |

**Sample Products Displayed on Home:**
- Grey jacket — £55.00
- Noir jacket — £60.00
- Striped top — £50.00

---

### 4.2 Products / Collection Page (`/collections/all`)

**Purpose:** Displays the complete catalog of products.

**Breadcrumb:** Home — Products

**Products in Catalog (7 total):**

| # | Product Name | Price (£) | Stock Status | Handle |
|---|--------------|-----------|--------------|--------|
| 1 | Black heels | 45.00 | In Stock | `flower-print-jeans` (quirky handle) |
| 2 | Bronze sandals | 39.99 | In Stock | `bronze-sandals` |
| 3 | Brown Shades | 20.00 | **Sold Out** | `brown-shades` |
| 4 | Grey jacket | 55.00 | In Stock | `grey-jacket` |
| 5 | Noir jacket | 60.00 | In Stock | `noir-jacket` |
| 6 | Striped top | 50.00 | In Stock | `striped-top` |
| 7 | White sandals | 25.00 | **Sold Out** | `white-sandals` |

**Page Elements:**
- Product grid (responsive)
- Product image thumbnail
- Product name
- Price
- \"Sold Out\" badge (where applicable)
- Click → Product Detail Page

---

### 4.3 Product Detail Page (PDP) (`/products/{handle}`)

**Purpose:** Detailed view of a single product, where users select variants and add to cart.

**Example:** https://sauce-demo.myshopify.com/products/noir-jacket

| Element | Description / Sample Data |
|---------|---------------------------|
| Breadcrumb | Home — Noir jacket |
| Product Images | Primary image + thumbnail gallery (zoomable) |
| Product Title | `Noir jacket` |
| Product Price | `£60.00` |
| **Variant: Size** | S / M / L |
| **Variant: Color** | Blue / Red |
| Variant Combinations | 6 total (S/Blue, M/Blue, L/Blue, S/Red, M/Red, L/Red) |
| All variants price | £60.00 each |
| Quantity Selector | Present |
| Add to Cart Button | Present |
| Product Description | Lorem-style placeholder text (Shopify default) |
| Social Share | Facebook / Twitter / Pinterest (Shopify default) |

**Notes for QA:**
- Variants must be tested for stock status, pricing, and availability.
- Some products may be single-variant (no size/color).
- Out-of-stock products disable Add to Cart.

---

### 4.4 Search Page (`/search`)

**Purpose:** Keyword-based product search.

**Example:** `/search?q=jacket` → returns 2 results (Grey jacket, Noir jacket)

| Element | Description |
|---------|-------------|
| Search Input | Accepts keyword queries |
| Results Display | Same card layout as collection page |
| Result Count | \"Showing results for {keyword}\" with count |
| Empty State | Message when no products match |
| Sort / Filter | (Depends on theme — usually basic) |

**Test Data Examples:**
- `jacket` → 2 results
- `sandals` → 2 results
- `xyz123` → 0 results (empty state)

---

### 4.5 Cart Page (`/cart`)

**Purpose:** Review selected items before proceeding to checkout.

| Element | Description |
|---------|-------------|
| Breadcrumb | Home — Cart |
| Page Title | \"My Cart\" |
| Empty State | \"It appears that your cart is currently empty! Continue Shopping.\" |
| Populated State | List of items with image, title, variant, quantity, price, remove |
| Subtotal | Total price of items |
| Update / Remove | Buttons to modify cart |
| Checkout Button | Proceeds to Shopify checkout |
| Continue Shopping | Redirects to Products |

---

### 4.6 Login Page (`/account/login`)

**Purpose:** Existing customers authenticate to access account.

| Element | Description |
|---------|-------------|
| Page Title | \"Customer Login\" |
| Breadcrumb | Home — Login |
| **Email Address** | Input, required, email format |
| **Password** | Input, masked, required |
| **Sign In Button** | Submits form |
| **Forgot your password?** | Inline link — reveals reset form |
| **Reset Form (Hidden by Default)** | Email + Submit + Cancel |
| **Create Account Link** | Redirects to /account/register |
| **Shop Social Login** | \"Log in with Shop\" alternative |

---

### 4.7 Register Page (`/account/register`)

**Purpose:** New customer account creation.

| Field | Type | Required |
|-------|------|----------|
| **First Name** | Text | Yes |
| **Last Name** | Text | Yes |
| **Email Address** | Email | Yes |
| **Password** | Password (masked) | Yes |
| **Create Button** | Submit | — |
| **Back to Login** | Link | — |

---

### 4.8 Checkout Flow (Shopify-hosted, `/checkout`)

Shopify provides a **standard 3-step checkout**:

| Step | Fields / Actions |
|------|------------------|
| **1. Information** | Contact email, shipping address (First name, Last name, Address, City, Postal Code, Country, Phone) |
| **2. Shipping** | Choose a shipping method (rates from Shopify) |
| **3. Payment** | Card (demo / test mode), billing address, Place Order |
| **4. Order Confirmation** | Order number, summary, email confirmation |


---

## 5. Global / Common UI Elements

Present across ALL pages:

| Component | Description |
|-----------|-------------|
| **Header** | Store name/logo, main navigation, search icon, account icon, cart icon (with item count) |
| **Breadcrumb** | Shows path (Home — Section — Page) |
| **Cart Widget** | \"Your cart is empty.\" / cart item count |
| **Footer** | Standard Shopify footer links (About, Contact, Policies) |
| **Blocked-by-extension overlay** | Not a real element — artifact of browser extensions (e.g. ad-blockers). Should be ignored in QA unless explicitly testing for it. |

---

## 6. User Roles / Personas

| Role | Access Rights |
|------|---------------|
| **Guest Visitor** | Browse, search, view products, add to cart, checkout as guest |
| **Registered Customer** | All guest rights + saved addresses, order history, faster checkout |
| **Admin (not in scope)** | Shopify Admin Panel (not accessible to QA testers of the storefront) |

---

## 7. Key Business Rules & Assumptions

1. 🛒 Cart persists across sessions (cookie-based).
2. 💷 All prices are displayed in **GBP (£)**.
3. 🚫 Out-of-stock products cannot be added to the cart.
4. 🔑 Password has no stated complexity rule (should be tested).
5. 📧 Email must be unique at registration.
6. 📦 Shipping methods depend on destination.
7. 🔐 Shopify handles all checkout & payment on its own secure infrastructure.
8. 🧾 Order confirmation emails are sent automatically.

---

## 8. Technical & Environmental Details

| Attribute | Value |
|-----------|-------|
| **Domain** | sauce-demo.myshopify.com |
| **Protocol** | HTTPS |
| **CDN** | Shopify CDN (`cdn/shop/...`) |
| **Frontend Framework** | Liquid templates (Shopify) |
| **Session Management** | Cookie-based (Shopify `_secure_session_id`) |
| **Payment Gateway** | Shopify Payments / Bogus Gateway (demo) |
| **Hosting** | Shopify (multi-tenant SaaS) |

---

## 9. Out-of-Scope for QA Testing

- Shopify Admin dashboard (backend)
- Third-party app integrations not visible on storefront
- Real payment processing (test with Bogus Gateway only)
- Email server / SMTP configuration
- Shopify platform-level bugs

---

## 10. QA Manual Roadmap (to be created next)

Based on this overview, the following test manuals will be produced:

| # | Manual Title | Status |
|---|--------------|--------|
| 01 | **Website Overview Document** *(this file)* | ✅ Done |
| 02 | Manual Test Cases — **Login & Authentication** | ✅ Done (separate file) |
| 03 | Manual Test Cases — **Registration** | ⏳ Planned |
| 04 | Manual Test Cases — **Home Page** | ⏳ Planned |
| 05 | Manual Test Cases — **Products / Collection Page** | ⏳ Planned |
| 06 | Manual Test Cases — **Product Detail Page (PDP)** | ⏳ Planned |
| 07 | Manual Test Cases — **Search** | ⏳ Planned |
| 08 | Manual Test Cases — **Cart** | ⏳ Planned |
| 09 | Manual Test Cases — **Checkout & Payment** | ⏳ Planned |
| 10 | Manual Test Cases — **Account / My Profile** | ⏳ Planned |
| 11 | **End-to-End (E2E) Scenarios** | ⏳ Planned |
| 12 | **Cross-Browser & Responsive Checklist** | ⏳ Planned |
| 13 | **Accessibility & Security Checklist** | ⏳ Planned |
| 14 | **Master Test Plan & Traceability Matrix** | ⏳ Planned |

---

## 11. Glossary

| Term | Meaning |
|------|---------|
| **PDP** | Product Detail Page |
| **PLP** | Product Listing Page (collection) |
| **SKU** | Stock Keeping Unit (unique product variant) |
| **AUT** | Application Under Test |
| **CTA** | Call To Action (buttons like Add to Cart) |
| **E2E** | End-to-End |
| **WCAG** | Web Content Accessibility Guidelines |
| **UAT** | User Acceptance Testing |

---

**End of Document**
"
Observation: Create successful: /app/manual_tests/01_Sauce_Demo_Website_Overview.md