---
id: 004-database
title: Database Schema & Data Models
description: Detailed specification of the Firebase Firestore collections, fields, and relationships.
type: doc
subtype: core
status: draft
sequence: 4
tags:
  - database
  - firestore
  - schema
createdAt: '2023-10-27T10:03:00Z'
updatedAt: '2023-10-27T10:03:00Z'
---

## 1. Introduction

This document defines the data models and schema for the Bali Dog Rescue platform, which will be implemented using **Firebase Firestore**. Firestore's NoSQL, document-based structure is well-suited for the flexible and scalable data requirements of this project. The following collections form the core of our application's data layer.

## 2. Core Collections

### 2.1. `users`

Stores information for all registered individuals, including adopters, donors, volunteers, and administrators.

*   **Description:** This collection is linked to Firebase Authentication UIDs. When a user signs up, a corresponding document is created here.
*   **Fields:**
    *   `id` (string, required): The unique user ID from Firebase Auth.
    *   `email` (email, required): The user's login email.
    *   `displayName` (string): The user's full name.
    *   `role` (enum, required): Defines user permissions. Values: `adopter`, `volunteer`, `donor`, `admin`.
    *   `createdAt` (timestamp, required): The timestamp of account creation.
    *   `preferences` (object): Stores notification preferences, e.g., `{ newsletter: true, adoptionUpdates: false }`.

### 2.2. `dogs`

Contains the complete profile for every dog under the care of the organization.

*   **Description:** This is the central collection for the adoption feature. Each document represents one dog.
*   **Fields:**
    *   `id` (string, required): A unique ID for the dog.
    *   `name` (string, required): The dog's name.
    *   `story` (richtext, required): The detailed biography and background of the dog.
    *   `adoptionStatus` (enum, required): The current status. Values: `Available`, `Pending Adoption`, `Adopted`.
    *   `photos` (array of strings, required): An array of URLs pointing to images stored in Cloudinary.
    *   `videos` (array of strings): An array of URLs for videos.
    *   `age` (string): e.g., 'Puppy', 'Young', 'Adult', 'Senior'.
    *   `gender` (enum, required): `Male` or `Female`.
    *   `size` (enum): `Small`, `Medium`, `Large`.
    *   `healthStatus` (richtext): Information on vaccinations, spay/neuter status, and known medical conditions.
    *   `temperament` (array of strings): Descriptive tags like `playful`, `calm`, `good with kids`.
    *   `postedAt` (timestamp, required): When the profile was created.

### 2.3. `adoption_applications`

Records all adoption applications submitted by users for specific dogs. This collection links users and dogs.

*   **Description:** A new document is created each time a user submits an application form.
*   **Fields:**
    *   `id` (string, required): A unique application ID.
    *   `userId` (reference, required): A reference to the document in the `users` collection.
    *   `dogId` (reference, required): A reference to the document in the `dogs` collection.
    *   `status` (enum, required): The application's workflow status. Values: `Pending Review`, `Under Review`, `Interview Scheduled`, `Approved`, `Rejected`, `Withdrawn`.
    *   `submittedAt` (timestamp, required): When the application was submitted.
    *   `answers` (object, required): A key-value map of the application questions and the user's answers.
    *   `notes` (richtext): Internal notes added by administrators during the review process.

### 2.4. `donations`

Logs all financial transactions made through the platform.

*   **Description:** This collection provides a record for financial reporting and for populating a user's donation history.
*   **Fields:**
    *   `id` (string, required): A unique ID for the donation.
    *   `userId` (reference): A reference to the `users` collection if the donor was logged in.
    *   `donorEmail` (email, required): The email used for the receipt, captured for all donors.
    *   `amount` (number, required): The donation amount.
    *   `currency` (string, required): e.g., 'USD', 'IDR'.
    *   `type` (enum, required): `one-time` or `recurring`.
    *   `fund` (enum): The specific fund targeted. Values: `general`, `medical`, `food`, `shelter`.
    *   `transactionId` (string, required): The unique ID from the Stripe transaction.
    *   `status` (enum, required): `completed`, `pending`, `failed`.
    *   `donatedAt` (timestamp, required): The timestamp of the transaction.

### 2.5. `volunteer_opportunities`

Defines the various roles and tasks available for volunteers.

*   **Description:** Managed by admins, these documents are displayed on the `/volunteer` page.
*   **Fields:**
    *   `id` (string, required): A unique ID for the opportunity.
    *   `title` (string, required): The role title, e.g., "Weekend Dog Walker".
    *   `description` (richtext, required): A detailed description of the role.
    *   `requirements` (array of strings): A list of required skills or attributes.
    *   `timeCommitment` (string): e.g., "4 hours per week".
    *   `status` (enum, required): `Open`, `Closed`.

### 2.6. `volunteer_applications`

Stores applications submitted by users for volunteer opportunities.

*   **Description:** This collection links users to specific volunteer roles they have applied for.
*   **Fields:**
    *   `id` (string, required): A unique application ID.
    *   `userId` (reference, required): Reference to the `users` collection.
    *   `opportunityId` (reference, required): Reference to the `volunteer_opportunities` collection.
    *   `status` (enum, required): `Pending Review`, `Accepted`, `Rejected`.
    *   `submittedAt` (timestamp, required): When the application was submitted.
    *   `answers` (object, required): The applicant's answers to questions like "Why do you want to volunteer?"