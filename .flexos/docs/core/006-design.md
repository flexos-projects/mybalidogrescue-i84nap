---
id: 006-design
title: Design System & Branding
description: The visual identity, color palette, typography, and overall user experience principles.
type: doc
subtype: core
status: draft
sequence: 6
tags:
  - design
  - branding
  - ui
  - ux
createdAt: '2023-10-27T10:05:00Z'
updatedAt: '2023-10-27T10:05:00Z'
---

## 1. Design Philosophy

The design of the Bali Dog Rescue platform must be **compassionate, hopeful, and engaging**. Our goal is to create a user experience that is both emotionally resonant and highly functional. The design should build trust, encourage action, and reflect the professional and caring nature of our organization. We will prioritize clarity, simplicity, and accessibility to ensure the platform is usable by a diverse, global audience.

**Core Principles:**

*   **Story-First:** The design will prioritize high-quality imagery and compelling narratives. Photography and videography of the dogs are our most powerful assets and should be featured prominently.
*   **Clarity Over Clutter:** Interfaces will be clean, with clear calls-to-action. We will avoid visual noise that could distract users from our primary goals: adoption, donation, and volunteering.
*   **Trust and Transparency:** The design must feel secure and professional, especially on pages involving payments (`/donate`) and personal information (`/auth`, `/dashboard`).
*   **Mobile-First:** With a global audience, we anticipate significant mobile traffic. All pages and components will be designed with a responsive, mobile-first approach to ensure a seamless experience on any device.

## 2. Branding & Vibe

*   **Vibe:** The overall feeling should be one of **hope and positivity**. While we are addressing a serious problem, the user should feel empowered and inspired to help, not discouraged by overwhelming sadness. The tone should be welcoming and encouraging.
*   **Logo:** A clean, simple logo that incorporates a dog silhouette and perhaps a heart or a subtle nod to Bali (e.g., a frangipani flower). It must be versatile for use on the website, social media, and merchandise.
*   **Imagery:** All photography should be high-quality, well-lit, and focus on the dogs' personalities. We want to show them as hopeful and resilient individuals deserving of a loving home.

## 3. Color Palette

The color palette is chosen to be modern, clean, and welcoming, reflecting the tropical environment of Bali while maintaining a professional feel.

*   **Primary Color:** `#06b6d4` (Cyan)
    *   **Usage:** Used for primary buttons, links, active navigation states, and key calls-to-action. It's an optimistic and trustworthy color that evokes the sea and sky.
*   **Accent Color:** `#f97316` (Orange)
    *   **Usage:** Used sparingly for secondary CTAs, highlights, or important notifications. It's a warm, energetic color that provides a strong contrast to the primary cyan.
*   **Neutral Dark:** `#1f2937` (Cool Gray)
    *   **Usage:** For all body text, headlines, and primary icons. It's a modern, legible alternative to pure black.
*   **Neutral Light:** `#f9fafb` (Off-White)
    *   **Usage:** For page backgrounds and content containers. It provides a clean, soft backdrop that allows the content and imagery to stand out.
*   **Supporting Colors:**
    *   **Success:** A gentle green (`#10b981`) for success messages and confirmations.
    *   **Warning/Error:** A soft red (`#ef4444`) for error messages and critical alerts.

## 4. Typography

Typography will be clean, modern, and highly legible across all devices.

*   **Font Family:** **Inter**
    *   **Rationale:** Inter is a variable font designed specifically for computer screens. It offers excellent readability at all sizes and weights, making it perfect for both UI elements and long-form content like dog stories.
*   **Hierarchy:**
    *   **Headings (h1, h2, h3):** Inter Bold, using a clear size scale (e.g., 36px, 24px, 20px) to establish a strong visual hierarchy.
    *   **Body Text:** Inter Regular, set at a comfortable size (16px) with adequate line spacing (1.5) for readability.
    *   **UI Elements (Buttons, Labels):** Inter Medium or SemiBold to ensure they are distinct and easy to read.

## 5. UI Components & Patterns

We will utilize a component-based approach, likely using a framework like Nuxt UI, to ensure consistency across the platform.

*   **Buttons:** Primary buttons will use the `#06b6d4` color with white text. Secondary buttons will be outlined or use the accent color. They will have clear hover and active states.
*   **Forms:** Inputs will be clean and spacious with clear labels and validation states. Multi-step forms (like the adoption application) will include a progress indicator.
*   **Cards:** Dog profiles (`/adopt`) and volunteer opportunities (`/volunteer`) will be displayed using a consistent card component, featuring an image, title, key details, and a clear link to the details page.
*   **Navigation:** A persistent sidebar or top navigation bar will provide easy access to Home, Adopt, Donate, and Volunteer. For logged-in users, a link to their Dashboard will be prominent.