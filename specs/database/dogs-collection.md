---
id: spec-collection-dogs
title: Dogs Collection Database Specification
description: Defines the structure and fields for the 'dogs' data collection in Firebase Firestore.
type: spec
subtype: database
status: draft
sequence: 4
tags: ["database", "collection", "dogs", "firestore"]
relatesTo: dog-adoption-profiles, adoption_applications
createdAt: 2023-10-27T10:00:00Z
updatedAt: 2023-10-27T10:00:00Z
---
This specification details the `dogs` collection, the central data repository for all rescue dogs managed by Bali Dog Rescue. Stored in Firebase Firestore, each document in this collection represents an individual dog available for adoption or currently under care. Key fields include a unique `id` for identification, the dog's `name`, and descriptive attributes like `breed`, `age` (categorized as Puppy, Young, Adult, Senior), `gender`, and `size`. A rich text `story` field provides their background and journey, while `healthStatus` captures detailed medical records. `temperament` is an array of tags for easy filtering and understanding. Visual content is crucial, so `photos` (URLs to Cloudinary) are required, and `videos` are optional. The `adoptionStatus` enum tracks their journey ('Available', 'Pending Adoption', 'Adopted'), and `location` notes their current physical placement. `postedAt` records the profile creation date. This collection is foundational, directly supporting the "Detailed Dog Adoption Profiles" feature and serving as a reference for `adoption_applications`, ensuring comprehensive and accessible information for both administrators and potential adopters.