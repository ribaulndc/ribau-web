# 🔄 RiBau Workflow - Visual Reference

Quick visual guide to understand how everything works together.

---

## 🎯 Complete System Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                         RIBAU PRODUCT SYSTEM                        │
└─────────────────────────────────────────────────────────────────────┘

┌──────────────────┐         ┌──────────────────┐         ┌──────────────────┐
│                  │         │                  │         │                  │
│  Google Sheets   │────────▶│  GitHub Actions  │────────▶│   GitHub Repo    │
│  (Volunteers)    │  Reads  │   (Every 30min)  │ Commits │  (products.csv)  │
│                  │  Data   │                  │  CSV    │                  │
└──────────────────┘         └──────────────────┘         └──────────────────┘
                                                                      │
                                                                      │ Triggers
                                                                      ▼
┌──────────────────┐         ┌──────────────────┐         ┌──────────────────┐
│                  │         │                  │  Reads  │                  │
│  GitHub Repo     │────────▶│     Netlify      │────────▶│   Vue Website    │
│  (Images)        │  Hosts  │   (Auto-deploy)  │  CSV    │  (Public Site)   │
│  (You manage)    │  Files  │                  │  &      │                  │
│                  │         │                  │  Images │                  │
└──────────────────┘         └──────────────────┘         └──────────────────┘
         ▲                                                         │
         │                                                         │
         │  Uploads Images                        Visitors See    │
         │                                        Products         │
         │                                                         ▼
    ┌──────────┐                                          ┌──────────────┐
    │   You    │                                          │   Visitors   │
    │ (Admin)  │                                          │   (Public)   │
    └──────────┘                                          └──────────────┘
```

---

## 📝 Adding New Product - Detailed Flow

```
STEP 1: VOLUNTEER PREPARES
┌─────────────────────────────────────────────┐
│ Volunteer takes/collects product photos    │
│ • 1-3 clear images                         │
│ • Good lighting, plain background          │
└─────────────────────────────────────────────┘
                    │
                    ▼
STEP 2: SEND TO YOU
┌─────────────────────────────────────────────┐
│ Volunteer sends to you via:                │
│ • WhatsApp / Email / Slack                 │
│ • Message: "Images for new blue leash"     │
└─────────────────────────────────────────────┘
                    │
                    ▼
STEP 3: YOU PROCESS IMAGES
┌─────────────────────────────────────────────┐
│ 1. Check last ID in Google Sheet (e.g. 025)│
│ 2. Next ID is 026                          │
│ 3. Rename images:                          │
│    • leash1.jpg → 026_1.jpg                │
│    • leash2.jpg → 026_2.jpg                │
│ 4. Optional: Optimize (TinyPNG.com)        │
│ 5. Move to: public/images/products/        │
│ 6. Git commit & push                       │
└─────────────────────────────────────────────┘
                    │
                    ▼
STEP 4: CONFIRM TO VOLUNTEER
┌─────────────────────────────────────────────┐
│ Reply: "✓ Images ready! Use ID 026"        │
└─────────────────────────────────────────────┘
                    │
                    ▼
STEP 5: VOLUNTEER ADDS TO SHEET
┌─────────────────────────────────────────────┐
│ Opens Google Sheet                         │
│ Adds new row:                              │
│ 026│Guinzaglio Blu│...│12.00│TRUE│FALSE   │
└─────────────────────────────────────────────┘
                    │
                    ▼
STEP 6: AUTOMATIC SYNC (30 minutes)
┌─────────────────────────────────────────────┐
│ GitHub Action runs automatically:          │
│ 1. Reads Google Sheet                      │
│ 2. Converts to CSV                         │
│ 3. Validates images exist                  │
│ 4. Commits to repo                         │
│ 5. Netlify auto-deploys                    │
└─────────────────────────────────────────────┘
                    │
                    ▼
STEP 7: LIVE ON WEBSITE! 🎉
┌─────────────────────────────────────────────┐
│ Product visible with:                      │
│ • Name, description, price                 │
│ • All 2 images in carousel                 │
│ • Contact form integration                 │
└─────────────────────────────────────────────┘
```

---

## ⏱️ Timing Breakdown

```
┌────────────────────────────────────────────────┐
│ Task                          │ Time           │
├───────────────────────────────┼────────────────┤
│ Volunteer takes photos        │ 5-10 minutes   │
│ Sends to you                  │ 1 minute       │
│ You process & upload images   │ 5 minutes      │
│ Volunteer adds to sheet       │ 2-3 minutes    │
│ Wait for sync                 │ 0-30 minutes   │
│ Netlify deployment            │ 1-2 minutes    │
├───────────────────────────────┼────────────────┤
│ TOTAL (worst case)            │ ~50 minutes    │
│ TOTAL (best case)             │ ~15 minutes    │
└───────────────────────────────┴────────────────┘
```

**Note:** Sync happens every 30 min, so could be instant or 30 min wait!

---

## 🔄 Data Flow Diagram

```
┌───────────────────────────────────────────────────────────────┐
│                      DATA SOURCES                            │
└───────────────────────────────────────────────────────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
        ▼                   ▼                   ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│ Google Sheet │    │ GitHub Repo  │    │   Netlify    │
│              │    │              │    │   Config     │
│ • id         │    │ • Images     │    │ • Forms      │
│ • name       │    │ • fallback   │    │ • Deploy     │
│ • price      │    │              │    │   settings   │
│ • category   │    │              │    │              │
│ • inStock    │    │              │    │              │
└──────────────┘    └──────────────┘    └──────────────┘
        │                   │                   │
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │   GitHub Actions      │
                │   (sync-sheets.js)    │
                │                       │
                │   Combines & Syncs    │
                └───────────────────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │   products.csv        │
                │   (Generated)         │
                └───────────────────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │   Vue Website         │
                │   • ProductCatalog    │
                │   • ProductCard       │
                │   • ContactForm       │
                └───────────────────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │   Public Website      │
                │   (Visitors See)      │
                └───────────────────────┘
```

---

## 🎭 User Roles & Responsibilities

```
┌─────────────────────────────────────────────────────────┐
│                     VOLUNTEERS                          │
├─────────────────────────────────────────────────────────┤
│ CAN DO:                                                 │
│ ✓ Add products to Google Sheet                         │
│ ✓ Edit product details (name, price, description)      │
│ ✓ Mark products as sold (inStock = FALSE)              │
│ ✓ Set featured products                                │
│ ✓ Create new categories                                │
│                                                         │
│ CANNOT DO:                                              │
│ ✗ Upload images (must coordinate with you)             │
│ ✗ Edit code or website directly                        │
│ ✗ Access GitHub repository                             │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                   YOU (ADMIN)                           │
├─────────────────────────────────────────────────────────┤
│ RESPONSIBILITIES:                                       │
│ ✓ Upload & optimize product images                     │
│ ✓ Assign product IDs                                   │
│ ✓ Maintain GitHub repository                           │
│ ✓ Monitor GitHub Actions for errors                    │
│ ✓ Train volunteers on Google Sheets                    │
│ ✓ Backup data periodically                             │
│                                                         │
│ OPTIONAL:                                               │
│ ○ Edit products directly in Google Sheet               │
│ ○ Update website code/styling                          │
│ ○ Configure Netlify settings                           │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                   AUTOMATED SYSTEM                      │
├─────────────────────────────────