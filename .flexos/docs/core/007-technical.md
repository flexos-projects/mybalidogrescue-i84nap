---
id: 007-technical
title: Technical Architecture & Stack
description: An overview of the frameworks, technologies, and services that will power the platform.
type: doc
subtype: core
status: draft
sequence: 7
tags:
  - tech-stack
  - architecture
  - firebase
  - nuxt
createdAt: '2023-10-27T10:06:00Z'
updatedAt: '2023-10-27T10:06:00Z'
---

## 1. Introduction

This document outlines the technical architecture and technology stack for the Bali Dog Rescue platform. The chosen stack is modern, scalable, and developer-friendly, leveraging serverless technologies to minimize infrastructure management and cost while maximizing performance and reliability.

## 2. Core Technology Stack

Our stack is built around the Vue.js ecosystem and the Google Firebase platform.

*   **Framework:** **Nuxt 4**
    *   **Rationale:** Nuxt provides a powerful, opinionated framework on top of Vue.js. Its features like file-based routing, server-side rendering (SSR) for improved SEO, and a robust module ecosystem make it ideal for building a performant and maintainable web application. SSR is particularly important for ensuring that dog profile pages are easily discoverable by search engines.

*   **Database:** **Firebase Firestore**
    *   **Rationale:** As a serverless, NoSQL database, Firestore offers real-time data synchronization, robust security rules, and automatic scaling. This is perfect for features like live updates on adoption application statuses and managing user-generated content. The schema is detailed in `004-database.md`.

*   **Authentication:** **Firebase Authentication**
    *   **Rationale:** Provides a secure, easy-to-implement authentication solution with built-in support for email/password, social providers (Google, etc.), and user management. It integrates seamlessly with Firestore security rules to protect user data.

*   **Hosting:** **Firebase Hosting**
    *   **Rationale:** Offers a global CDN, free SSL certificates, and simple, one-command deployments. Its integration with Firebase Cloud Functions allows us to easily build out our backend logic.

## 3. Key Packages & Libraries

*   **UI Component Library:** **Nuxt UI**
    *   **Rationale:** A first-party component library for Nuxt that is built on top of Tailwind CSS. It provides a set of accessible, themeable, and production-ready components (buttons, forms, modals) that will accelerate development and ensure design consistency, as outlined in `006-design.md`.

*   **State Management:** **Pinia**
    *   **Rationale:** The official state management library for Vue. It offers a simple, intuitive, and type-safe way to manage global application state, such as the current user's authentication status or profile information.

*   **Utility Library:** **VueUse**
    *   **Rationale:** A collection of essential Vue Composition API utilities that will help with tasks like interacting with browser APIs, managing state, and handling user inputs, reducing the amount of boilerplate code we need to write.

## 4. API Integrations & Services

*   **Payment Processing:** **Stripe**
    *   **Integration:** We will use `Stripe.js` on the frontend to securely collect payment information, ensuring that sensitive card details never touch our servers. A Firebase Cloud Function will be used as a backend endpoint to create payment intents and process transactions via the Stripe API. This is the backbone of the **Make a Donation Flow** (`005-flows.md`).

*   **Media Management:** **Cloudinary**
    *   **Integration:** All dog photos and videos will be uploaded directly from the admin panel to Cloudinary. Cloudinary provides robust services for image/video storage, optimization, and transformation. Using Cloudinary offloads media hosting from our primary application server and allows for on-the-fly image resizing to optimize page load times, which is critical for the `/adopt` and `/adopt/[id]` pages.

*   **Transactional Emails:** **SendGrid / Resend**
    *   **Integration:** We will use a dedicated email service for all transactional emails (e.g., account verification, donation receipts, application status updates). A Firebase Cloud Function will be triggered by events in Firestore (like a status change in `adoption_applications`) and will use the chosen email provider's API to send templated, reliable emails.

## 5. Development & Deployment

*   **Version Control:** The codebase will be hosted on GitHub.
*   **CI/CD:** GitHub Actions will be configured for continuous integration and deployment. Every push to the `main` branch will automatically trigger a build and deploy the latest version to Firebase Hosting.
*   **Environment Variables:** We will manage environment variables (`.env` files) for different environments (development, staging, production) to handle API keys and other sensitive configuration details securely.