# Product Requirements Document: Levercast (Consolidated MVP)

## 1. Elevator Pitch

Levercast is a web application designed for busy entrepreneurs, solopreneurs, and content creators to streamline their social media workflow. It allows users to quickly capture ideas via text or voice, leverages AI and customizable templates to transform these thoughts into polished posts optimized for multiple platforms (starting with LinkedIn and Twitter), facilitates previewing and editing, supports image handling, and enables direct scheduling and publishing—saving significant time while amplifying online presence.

## 2. Who is this app for?

* **Primary:** Entrepreneurs, Solopreneurs, and Founders with limited time for social media management.
* **Secondary:** Content Creators, Marketers, and Professionals seeking efficient multi-platform publishing and brand building.
* **Initial Platform Focus:** Users active on LinkedIn and Twitter.

## 3. Functional Requirements

* **Idea Capture:**
    * Text input via a prominent input box.
    * Voice-to-text input capability.
    * Ability to upload images (e.g., JPG, PNG) alongside text ideas.
* **Idea Storage:**
    * Captured ideas (text, associated image) are saved as drafts for later processing or refinement.
* **Content Transformation (LLM-Powered):**
    * Process raw input using an LLM based on user-selected custom templates.
    * Generate optimized post variations tailored for LinkedIn and Twitter (MVP).
* **Template Management:**
    * Users can create, save, edit, and manage custom prompt templates to guide AI formatting (tone, style, length, etc.).
* **Preview & Editing:**
    * Display generated posts in previews that accurately mimic the native look and feel of LinkedIn and Twitter.
    * Allow inline editing of generated text content within the previews.
* **Image Handling:**
    * Associate uploaded images with generated posts.
    * Automatically adapt images (e.g., basic resizing/cropping) to fit platform best practices during preview/publishing.
* **Publishing & Scheduling:**
    * Securely connect LinkedIn and Twitter accounts via OAuth.
    * Directly publish finalized posts to selected platforms.
    * Schedule posts for future publication at a specified date and time.
* **Basic Analytics (MVP):**
    * Track and display basic engagement metrics for published posts (e.g., views/reads).
* **Platform & Design:**
    * Web application.
    * Responsive design for usability on desktop and mobile browsers.

## 4. User Stories (MVP)

* As a user, I want to quickly type or speak my raw ideas for social media content into the app, so I don't lose inspiration.
* As a user, I want to upload an image related to my idea, so it can be part of the final post.
* As a user, I want my captured ideas saved as drafts, so I can come back to refine or process them later.
* As a user, I want to create and apply custom templates, so the AI generates content in my preferred style for different platforms.
* As a user, I want the app to automatically generate post versions optimized for LinkedIn and Twitter from my single input, saving me manual effort.
* As a user, I want to see realistic previews of how my posts will look on LinkedIn and Twitter, including adapted images.
* As a user, I want to edit the generated text directly within the previews, so I can make final tweaks easily.
* As a user, I want to securely connect my LinkedIn and Twitter accounts, so the app can publish on my behalf.
* As a user, I want to publish posts immediately or schedule them for a future date and time, so I can maintain a consistent posting cadence.
* As a user, I want to see basic metrics (like views/reads) on my published posts, so I can understand their reach.

## 5. User Interface (High-Level)

* **Overall:** Clean, intuitive, minimalist web interface focused on efficient workflow (idea -> publish). Responsive layout.
* **Dashboard/Main View:**
    * Prominent idea capture area (text input, voice recording button, image upload).
    * Access to saved drafts/ideas.
    * Overview of scheduled and recently published posts.
    * Access point for template management.
* **Content Generation/Editing View:**
    * Input display area.
    * Template selection mechanism.
    * Preview panel showing generated posts styled for LinkedIn and Twitter (side-by-side or tabbed).
    * Inline editing capabilities within previews.
    * Publishing controls (Publish Now, Schedule).
* **Scheduling View:**
    * A calendar or list view displaying scheduled posts.
    * Ability to view, edit, or cancel scheduled posts.
* **Template Manager:**
    * Interface to create, view, edit, and delete custom prompt templates.
* **Analytics Display:**
    * Simple display integrated into the dashboard or post history showing view/read counts.
* **Settings:**
    * Manage connected social media accounts (OAuth).
    * User profile and potentially notification preferences.