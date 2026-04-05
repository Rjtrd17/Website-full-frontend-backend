# Shri Harsidhdhi Mataji Temple Website
A comprehensive, bilingual (Gujarati & English) website built for the revered Shri Harsidhdhi Mataji Temple (Koyala Dungar, Miyani). This static HTML-based project provides information for devotees, rich content on Temple history, Aarti & Garba texts, live Darshan features, and an independent administrative portal.

## 🗂️ Project Structure

The project currently operates as a fast, static front-end deployment, with separated domains for public access and secure administrative features.

- `harsidhdhi-mataji-temple-website.html`: The main public-facing web platform. Includes responsive UI/UX, integrated bilingual text toggling, Garba/Aarti references, image galleries, and secure donation structures.
- `admin.html`: The dedicated, password-protected administrative console. Visually distinct (dark theme) from the public site, used to manage streaming links, gallery uploads, and analyze donation metadata.
- `*.png`: All high-definition, meticulously generated image assets used across the web app.
- `PAYMENT_SETUP_GUIDE.md`: A step-by-step developer guide meant for setting up a Razorpay payment gateway to process and authenticate live donations. It also covers establishing a NodeMailer/SendGrid pipeline for generating automatic receipt emails.
- `POSTGRESQL_SETUP_GUIDE.md`: A comprehensive documentation guide addressing the transition from a static setup to a robust PostgreSQL-backed full-stack platform.

## ✨ Features

*   **Bilingual System:** Fully functional class-based language toggle (`.gu` and `.en`).
*   **Cultural Content:** Authentic Stuti, Maha-Aarti, and 12 devoted Garbas formatted beautifully.
*   **Aesthetic Identity:** Saffron-gold-crimson theme matching the spiritual ambiance.
*   **Interactive Maps:** A rich "Explore & Visit" itinerary section detailing nearby historical elements like Bileshwar Mahadev and the history with Jam Saheb & Ajay Jadeja.
*   **Decoupled Administration:** Built-in console for administrators to update 'Live Darshan' streams independently.

## 🚀 Future Integration Roadmap

This repository sets up the **frontend architecture**. To make the platform fully live and dynamic, the backend must be integrated following the markdown documents provided:

1.  **Backend Migration:** The admin console's "Save" functionality currently fires a static client-side alert. Using the `POSTGRESQL_SETUP_GUIDE.md`, deploy a Node.js/Express.js backend server.
2.  **Payment Processing:** Adopt the structure detailed in `PAYMENT_SETUP_GUIDE.md` to map public donations securely via Razorpay Webhooks. 
3.  **Authentication:** Lock the `admin.html` page using JSON Web Tokens (JWT) or Passport.js to shield the backend operations from unauthorized users.

## 📦 Deploying to GitHub/Pages

Since the public website operates statically out-of-the-box, it is fully compatible with free hosting solutions like **GitHub Pages** or **Vercel**.
1. Navigate to your Repo Settings on GitHub.
2. Under "Pages", configure the source to build from the main branch.
3. Once deployed, anyone can interact with `harsidhdhi-mataji-temple-website.html` instantly.

*(Note: temporary `.py` editing scripts used during development are ignored via `.gitignore` and omitted from deployment.)*
