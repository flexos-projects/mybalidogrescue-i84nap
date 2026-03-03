---
id: 005-flows
title: User & System Flows
description: Step-by-step descriptions of key user journeys and system processes.
type: doc
subtype: core
status: draft
sequence: 5
tags:
  - flows
  - user-journey
  - process
createdAt: '2023-10-27T10:04:00Z'
updatedAt: '2023-10-27T10:04:00Z'
---

## 1. Introduction

This document details the critical user and system flows for the Bali Dog Rescue platform. These flows describe the step-by-step processes for key interactions, ensuring a logical and seamless experience. They serve as a blueprint for development and user experience design.

## 2. New User Onboarding & Signup Flow

*   **Trigger:** A new visitor clicks 'Sign Up' in the header or attempts an action (e.g., 'Apply to Adopt') that requires an account.
*   **Goal:** To register the user, verify their account, and introduce them to the platform's core functions.
*   **Steps:**
    1.  **Initiate Signup (User):** User clicks the 'Sign Up' button.
    2.  **Present Form (System):** System displays the registration form on the `/auth` page, offering options for email/password or social login (Google).
    3.  **Complete Form (User):** User enters their name, email, and a secure password, or authenticates via the social provider.
    4.  **Create Account (System):**
        *   The system calls Firebase Authentication to create the user account.
        *   Upon success, it creates a corresponding document in the `users` collection in Firestore with a default `role` of 'adopter'.
        *   If email/password was used, an email verification link is sent.
    5.  **Email Verification (User):** User clicks the verification link in their email, which directs them back to the site and updates their `emailVerified` status in Firebase.
    6.  **First Login & Onboarding (System):** The user is automatically logged in and redirected to their new, empty `/dashboard`. The system triggers the **Interactive Onboarding Walkthrough**, a brief tour highlighting the 'Adopt', 'Donate', and 'Volunteer' sections.
    7.  **Flow Complete (User):** The user can skip or complete the tour and is now free to explore the platform as an authenticated user.

## 3. Adopt a Dog Application Flow

*   **Trigger:** A logged-in user clicks 'Apply to Adopt' on a specific dog's profile page (`/adopt/[id]`).
*   **Goal:** To enable a potential adopter to submit a comprehensive application for a specific dog.
*   **Steps:**
    1.  **Browse & Select (User):** User navigates the `/adopt` page, uses filters, and clicks on a dog they are interested in.
    2.  **Initiate Application (User):** On the dog's profile, the user clicks the 'Apply to Adopt' button.
    3.  **Display Form (System):** The system presents a multi-step adoption application form. User and dog IDs are pre-filled.
    4.  **Complete Application (User):** The user fills out all required fields, which may include personal details, living situation, pet history, and references.
    5.  **Submit Application (User):** User reviews their answers and clicks 'Submit'.
    6.  **Process Submission (System):**
        *   The system validates the form data.
        *   A new document is created in the `adoption_applications` collection with the `userId`, `dogId`, `answers`, and a default `status` of 'Pending Review'.
        *   The system sends a confirmation email to the user, acknowledging receipt and setting expectations for the review timeline.
        *   A notification is triggered for administrators in the `/admin` panel.
    7.  **Update Dashboard (System):** The user is redirected to their `/dashboard`, where the new application appears in their 'Adoption Application Status' section.

## 4. Make a Donation Flow

*   **Trigger:** Any user (logged in or guest) clicks a 'Donate' button.
*   **Goal:** To facilitate a secure and easy financial contribution.
*   **Steps:**
    1.  **Access Donation Page (User):** The user lands on the `/donate` page.
    2.  **Select Donation Details (User):** The user selects a donation amount, frequency (one-time/monthly), and an optional fund to support.
    3.  **Enter Payment Information (User):** The user enters their name, email, and credit card details into the secure Stripe Elements form.
    4.  **Confirm & Process (User/System):** The user clicks 'Donate Now'. The system securely sends the payment information to the Stripe API for processing.
    5.  **Handle Response (System):**
        *   **On Success:** The system receives a success confirmation from Stripe. It creates a new document in the `donations` collection with all relevant details (`amount`, `donorEmail`, `transactionId`, `status: 'completed'`). It displays a 'Thank You' message to the user and sends a receipt to their email.
        *   **On Failure:** The system receives an error from Stripe and displays a user-friendly message (e.g., "Your card was declined. Please try another card.").
    6.  **Update History (System):** If the user was logged in, the new donation is added to their history on the `/dashboard` page.

## 5. Admin Manages Applications Flow

*   **Trigger:** An administrator logs in and navigates to the 'Adoption Applications' section of the `/admin` panel.
*   **Goal:** To allow admins to efficiently review, manage, and communicate about adoption applications.
*   **Steps:**
    1.  **View Applications (User - Admin):** The admin sees a list of all applications from the `adoption_applications` collection, sortable by `status` or `submittedAt`.
    2.  **Review Application (User - Admin):** The admin clicks on an application to view all the applicant's `answers`, linked user profile, and the profile of the dog in question.
    3.  **Update Status (User - Admin):** The admin uses a dropdown menu to change the application `status` (e.g., from 'Pending Review' to 'Under Review', or to 'Interview Scheduled').
    4.  **Trigger Notification (System):** When the `status` field is updated in Firestore, a system trigger (e.g., Firebase Function) sends an automated email notification to the applicant, informing them of the change and directing them to their dashboard for more details.
    5.  **Add Notes (User - Admin):** The admin can add internal `notes` to the application document for team collaboration (e.g., "Interviewed on Oct 27, seems like a good fit.").
    6.  **Finalize Application (User - Admin):** The admin sets the final status to 'Approved' or 'Rejected', triggering a final notification to the applicant.