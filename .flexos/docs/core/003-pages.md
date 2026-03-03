---
id: 003-pages
title: Pages & Information Architecture
description: A sitemap and description of each page within the Bali Dog Rescue platform.
type: doc
subtype: core
status: draft
sequence: 3
tags:
  - pages
  - architecture
  - sitemap
createdAt: '2023-10-27T10:02:00Z'
updatedAt: '2023-10-27T10:02:00Z'
---

## 1. Introduction

This document outlines the information architecture of the Bali Dog Rescue platform, detailing the primary pages, their purpose, and their key sections. The structure is designed to be intuitive for all user types, guiding them logically through the core functions of adoption, donation, and volunteering.

## 2. Public Pages (No Authentication Required)

These pages are accessible to all visitors and form the public-facing identity of the organization.

### 2.1. Home (`/` or `/home`)

*   **Purpose:** The main landing page. It must immediately convey our mission, build an emotional connection, and provide clear calls-to-action to the platform's key areas.
*   **Sections:**
    *   **Hero Section:** A powerful, full-width image or video with the mission statement and primary CTAs: "Adopt a Friend", "Donate Now", "Volunteer With Us".
    *   **Featured Adoptable Dogs:** A curated selection of 3-4 dogs from the `dogs` collection with `adoptionStatus: 'Available'` to encourage immediate exploration.
    *   **Impact & Success Stories:** Snippets showcasing our impact (e.g., "X Dogs Rescued This Year") and links to recent success stories or blog posts.
    *   **About Us Summary:** A brief introduction to our story and team, linking to a full 'About Us' page.

### 2.2. Adoptable Dogs (`/adopt`)

*   **Purpose:** To provide a comprehensive, filterable gallery of all dogs available for adoption.
*   **Sections:**
    *   **Filter & Search Bar:** Allows users to filter the dog list by `age`, `size`, `gender`, and possibly `location`.
    *   **Dog Card Grid:** A responsive grid displaying a primary photo, name, age, and adoption status for each dog. Each card links to the individual dog profile page.
    *   **Pagination / Load More:** To handle a large number of dogs without overwhelming the user.

### 2.3. Dog Profile (`/adopt/[id]`)

*   **Purpose:** A dynamic page dedicated to a single dog, providing all necessary information for an adoption decision.
*   **Sections:**
    *   **Photo/Video Gallery:** The main visual element, showcasing the dog's personality.
    *   **Detailed Information:** Name, breed, age, size, and a detailed biography/story.
    *   **Health & Temperament:** Clear sections for medical history and personality traits.
    *   **Primary CTA:** A prominent "Apply to Adopt" button that is the main goal of this page.

### 2.4. Donate (`/donate`)

*   **Purpose:** A dedicated, secure page for collecting financial contributions.
*   **Sections:**
    *   **Impact Statement:** Text and visuals explaining *why* donations are critical.
    *   **Donation Form:** The interactive component for selecting amount, frequency (one-time/recurring), and specific funds. This is powered by the `secure-donation-platform` feature.
    *   **Payment Integration:** Secure fields for payment information, handled by Stripe.js.

### 2.5. Volunteer (`/volunteer`)

*   **Purpose:** To inform and recruit potential volunteers.
*   **Sections:**
    *   **Overview of Volunteering:** An introduction to the types of help needed.
    *   **List of Opportunities:** A dynamic list of open positions pulled from the `volunteer_opportunities` collection.
    *   **Application Form:** A form for users to apply for a specific role.

### 2.6. Login / Sign Up (`/auth`)

*   **Purpose:** A single entry point for user authentication.
*   **Sections:**
    *   Tabs for Login and Sign Up forms.
    *   Password reset functionality.
    *   Social login options (Google, etc.).

## 3. Authenticated Pages (Login Required)

These pages provide a personalized experience for registered users.

### 3.1. My Dashboard (`/dashboard`)

*   **Purpose:** The user's personal hub for all their interactions with the platform.
*   **Sections:**
    *   **Adoption Application Status:** A tracker showing any submitted applications and their current `status` (e.g., 'Pending Review', 'Interview Scheduled').
    *   **Donation History:** A list of all past donations made while logged in.
    *   **Volunteer Schedule:** For accepted volunteers, this will show upcoming shifts or tasks.
    *   **Quick Links:** Easy navigation to `/settings` and other relevant areas.

### 3.2. Settings (`/settings`)

*   **Purpose:** To allow users to manage their account details and preferences.
*   **Sections:**
    *   **Profile Information Editor:** Form to update name, email, etc.
    *   **Password Change Form.**
    *   **Notification Preferences:** Toggles for different email communications.

## 4. Admin Panel (`/admin`)

*   **Purpose:** A restricted-access area for staff to manage all platform content and operations. This is the backend interface for our team.
*   **Sections:**
    *   **Management Dashboards:** Separate sections for managing `dogs`, `adoption_applications`, `donations`, and `volunteer_opportunities`.