# Greenland Legacy International School Website

A premium, high-performance, responsive single-page website for **Greenland Legacy International School** located in Kpeve, Volta Region, Ghana (Behind Power House, off Dudome Road). 

This website is custom redesigned to reflect a modern, high-end, glassmorphic aesthetic while retaining the school's real flyers and images as the primary visual assets. The site is optimized for academic recruitment and presents a deep integration of practical agricultural education (Poultry, Pig Farming, Greenhouse Technology, and Agribusiness) alongside its standard academic programs (Creche, KG, Primary, and JHS).

---

## 🌟 Key Features

1. **Premium Aesthetic & Layout:**
   - **Glassmorphic Design System:** Cards, header navigation, and overlay modal popups use blur backdrops, subtle semi-transparent borders, and gold-hued drop shadows.
   - **Dynamic Animations:** Features custom hover zooms, hover border-glow transitions, scroll-driven fade-up animations (using JavaScript `IntersectionObserver`), and a floating CTA animation.
   - **Contained Watermark Hero:** The hero section uses the school logo in a faint, contained, transparent background layout (`opacity: 0.08` watermark) with a darkened overlay ensuring optimal text readability.

2. **Smart Responsive Navigation:**
   - **Circular Expanding Menu:** On mobile devices, the mobile navigation is an overlay that elegantly expands outward circularly from the hamburger button.
   - **Body Scroll-Locking:** The page scroll is locked when the mobile nav menu is expanded or when the enrollment modal is open to ensure UX consistency.
   - **Active Navigation Highlighting:** Active page sections are highlighted in the navigation bar automatically as the user scrolls.

3. **Pure CSS Image Cropping:**
   - Instead of loading multiple cropped images, the website directly references the original flyer images (`images/132307.jpg` to `images/132311.jpg`) and uses CSS `object-fit: cover` combined with `object-position` coordinates to crop and center-focus key elements (such as targeting specific farm animals/structures on a flyer).

4. **Interactive Gallery & Lightbox:**
   - A grid showcasing actual school flyers. Clicking any flyer opens it in a full-screen, responsive blur-backdrop Lightbox modal that supports touch/click dismissals and the `Escape` key.

5. **Integrated Enrollment Modal Form:**
   - Opens via gold-contrast CTA buttons.
   - Restricts scrolling on the background page while active.
   - Validates user input in real-time (Ghana-format phone check `0XXXXXXXXX`, email regex check, required fields check) and displays target-specific red validation messages.
   - Safely escapes strings using custom HTML entity escaping to prevent XSS before logging sanitized application data.

6. **Floating WhatsApp Widget:**
   - A persistent floating widget pointing to the school's WhatsApp line (`+233533014819`) with custom animations and a hover-revealed glassmorphic tooltip text: *"Chat with us on WhatsApp"*.

---

## 🛡️ Security Implementations

This static website implements essential frontend security controls to keep the application resilient against common web vulnerabilities:

* **Cross-Site Scripting (XSS) Mitigation:**
  - A custom input sanitizer function (`escapeHTML`) is used to convert special characters (`&`, `<`, `>`, `'`, `"`) into safe HTML entities. This prevents any malicious string payloads from executing if form fields are rendered dynamically or processed.
* **Content Security Policy (CSP):**
  - Configured via a `<meta>` tag in the `<head>` of the page:
    ```html
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://cdnjs.cloudflare.com https://fonts.googleapis.com; font-src 'self' https://cdnjs.cloudflare.com https://fonts.gstatic.com; img-src 'self' data:; media-src 'none'; frame-src 'none'; object-src 'none'; base-uri 'self'; form-action 'self';">
    ```
  - **Resource Isolation:** Disables flash objects (`object-src 'none'`), frame embedding (`frame-src 'none'`), and media imports (`media-src 'none'`).
  - **Redirect Prevention:** Restricts forms from submitting to unauthorized endpoints using `form-action 'self'`, and blocks path hijacking using `base-uri 'self'`.
* **Subresource Integrity (SRI):**
  - CDN styles (Font Awesome) utilize secure `integrity` check hashes along with `crossorigin="anonymous"` and `referrerpolicy="no-referrer"` to verify that third-party resources haven't been tampered with or intercepted.
* **Tabnabbing Protection:**
  - All external anchor tags (e.g., the WhatsApp floating button) specify `rel="noopener noreferrer"` to prevent the target page from obtaining window reference access and hijacking the original browser tab.

---

## 📂 Project Structure

```text
GREENLAND_LEGACY/
├── index.html                  # Single-file main web application (HTML, CSS, JS)
├── README.md                   # Codebase documentation
└── images/                     # Folder containing original flyers and logo assets
    ├── logo_transparent.png    # Background-removed official school logo
    ├── 132307.jpg              # Original greenhouse flyer (used for greenhouse cards)
    ├── 132308.jpg              # Original admissions flyer (used for agribusiness card)
    ├── 132309.jpg              # Original poultry/pig flyer (used for farming focus cards)
    ├── 132310.jpg              # Original farming flyer (used in the gallery)
    └── 132311.jpg              # Original school flyer containing logo details
```

---

## 🚀 Local Setup and Hosting

### 1. Simple Local Opening
Since this is a static single-page app, you can test it directly:
1. Double-click `index.html` or drag it into any modern web browser (Chrome, Firefox, Edge, Safari).
2. *Note: Browser security policies on file protocol (`file:///`) might restrict certain strict CSP features locally, which is normal.*

### 2. Local Web Server (Recommended)
To serve the website over HTTP and fully activate all CSP directives:
* Using Python:
  ```bash
  python3 -m http.server 8000
  ```
  Open `http://localhost:8000` in your web browser.
* Using Node.js (`live-server`):
  ```bash
  npx live-server
  ```

### 3. Production Deployment
To launch the website for public enrollment:
1. Upload `index.html` and the `images/` directory to any static web hosting provider (e.g., Cloudflare Pages, Netlify, Vercel, Firebase Hosting, or GitHub Pages).
2. Ensure the relative links to assets in `images/` are preserved.
