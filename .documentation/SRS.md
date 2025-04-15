# Levercast - Software Requirements Specification (SRS)

This document outlines the technical specifications for the Levercast application MVP, based on the defined Product Requirements Document (PRD) and User Interface Description Document (UIDD - Celestial Flow).

## System Design

* **Overview:** A web application comprising a static frontend, a backend API, a Backend-as-a-Service (BaaS) layer, and integrations with external APIs.
* **Frontend:** Client-side application built with HTML, CSS, and JavaScript, responsible for UI rendering and user interaction. Served as static files.
* **Backend API:** A custom Node.js API (likely using Express.js) responsible for business logic, interacting with the LLM, handling social media publishing workflows, and communicating with the database via the BaaS layer.
* **BaaS (Supabase):** Provides core services including PostgreSQL database, user authentication, and potentially object storage (for images).
* **External APIs:**
    * Google Gemini API: For content generation based on user input and templates.
    * LinkedIn API & Twitter (X) API: For publishing posts and potentially fetching analytics data.

## Architecture pattern

* **Primary:** Client-Server Architecture.
* **Frontend:** Standard static web hosting model.
* **Backend:** Monolithic API (for MVP scope) built on Node.js, exposing RESTful endpoints.
* **BaaS Integration:** Supabase acts as a service layer for authentication and database persistence, accessed by both frontend (Auth) and backend (DB operations).

## State management

* **Client-Side (Frontend):** Managed using plain JavaScript variables, objects, and potentially modules. State related to UI (e.g., open modals, form inputs) is handled directly in JS. Temporary session information (like JWT) managed by the Supabase Auth JS library. `localStorage` or `sessionStorage` might be used sparingly for non-sensitive UI state persistence if needed.
* **Server-Side (Backend):** The Node.js API is designed to be stateless. Each API request from the client contains all necessary information (including JWT for authentication) to be processed independently.

## Data flow

* **Authentication:** User interacts with Supabase Auth (via Supabase JS library) -> Supabase handles login/signup -> JWT stored client-side -> JWT sent in `Authorization` header to Backend API -> Backend API verifies JWT via Supabase.
* **Idea Generation:** User Input (HTML Form) -> JS sends data to Backend API (`/api/posts/generate`) -> Backend API validates, fetches template, calls Google Gemini API -> Gemini returns formatted content -> Backend API sends previews back to Frontend JS -> JS updates UI.
* **Saving Post (Draft/Scheduled):** User action -> JS sends post data to Backend API (`POST /api/posts` or `PUT /api/posts/:id`) -> Backend API saves data to Supabase DB.
* **Publishing:** User clicks Publish -> JS sends request to Backend API (`POST /api/posts/:id/publish`) -> Backend API retrieves post data & stored OAuth tokens from Supabase DB -> Backend API calls relevant Social Media API (LinkedIn/Twitter) -> Backend API updates post status in Supabase DB.
* **Image Upload:** User uploads image -> JS sends image data (potentially directly to Supabase Storage if configured, or via Backend API) -> URL stored with post data in Supabase DB.

## Technical Stack

* **Frontend:** HTML5, CSS3, JavaScript (ES6+)
* **Backend:** Node.js (using Express.js recommended)
* **Database & BaaS:** Supabase (PostgreSQL, Supabase Auth, Supabase Storage)
* **LLM API:** Google Gemini API
* **Social APIs:** LinkedIn API, Twitter API (X API)
* **Hosting:** TBD (e.g., Frontend: Netlify/Vercel; Backend API: Render/Heroku/Fly.io/Supabase Edge Functions; Supabase handles DB/Auth/Storage)

## Authentication Process

* **User Authentication:** Handled primarily by Supabase Auth (Email/Password, potentially Social Logins like Google). Supabase JS library manages client-side sessions and JWTs.
* **API Authentication:** Custom Backend API endpoints are protected. Requests must include a valid Supabase JWT in the `Authorization: Bearer <token>` header. The backend verifies the JWT using Supabase project keys.
* **Social Media Authorization (OAuth 2.0):**
    * User initiates connection flow from frontend settings.
    * Backend API handles the OAuth 2.0 flow (redirects, callback handling) with LinkedIn/Twitter.
    * Securely stores obtained access tokens and refresh tokens (encrypted) in the Supabase database, associated with the `user_id`. These tokens are used by the backend for publishing actions.

## Route Design

* **Frontend Routes (Conceptual Pages - served via static HTML/JS):**
    * `/` or `/dashboard`: Main application view (Idea Input, Recent Posts)
    * `/login`: User login page (likely handled by Supabase Auth UI/redirects)
    * `/signup`: User signup page (likely handled by Supabase Auth UI/redirects)
    * `/templates`: Template management view
    * `/schedule`: Scheduling calendar/list view
    * `/analytics`: Analytics dashboard view
    * `/settings`: User settings (profile, connected accounts)
* **Backend API Routes (Prefix: `/api/v1`):**
    * `POST /posts/generate`: Generate post previews via LLM.
    * `POST /posts`: Create a new post (draft/scheduled).
    * `GET /posts`: List user's posts.
    * `GET /posts/:id`: Get a specific post.
    * `PUT /posts/:id`: Update a post.
    * `DELETE /posts/:id`: Delete a post.
    * `POST /posts/:id/publish`: Trigger publishing of a post.
    * `GET /templates`: List user's templates.
    * `POST /templates`: Create a new template.
    * `PUT /templates/:id`: Update a template.
    * `DELETE /templates/:id`: Delete a template.
    * `GET /analytics`: Get analytics data (requires integration logic).
    * `POST /auth/connect/:platform`: Initiate OAuth connection (platform = linkedin/twitter).
    * `GET /auth/callback/:platform`: Handle OAuth callback.
    * `DELETE /auth/disconnect/:platform`: Disconnect a social account.
    * *(Protected routes require JWT validation)*

## API Design

* **Style:** RESTful principles.
* **Data Format:** JSON for request and response bodies.
* **Authentication:** JWT (Supabase) via `Authorization: Bearer <token>` header for protected routes.
* **Stateless:** Backend API does not maintain session state between requests.
* **Versioning:** Via URL prefix (e.g., `/api/v1`).
* **Error Handling:** Use standard HTTP status codes (2xx for success, 4xx for client errors, 5xx for server errors) and provide meaningful JSON error messages.

## Database Design ERD (Supabase/PostgreSQL - Textual Description)

* **users:** (Implicitly managed by Supabase `auth.users`)
    * `id (UUID, PK)`: References `auth.users.id`.
    * *(Other profile fields like `name`, `avatar_url` might be added here or rely on `auth.users.raw_user_meta_data`)*
* **templates:**
    * `template_id (UUID, PK)`
    * `user_id (UUID, FK references auth.users.id)`
    * `name (TEXT, NOT NULL)`
    * `prompt (TEXT, NOT NULL)`
    * `created_at (TIMESTAMPTZ, default now())`
    * `updated_at (TIMESTAMPTZ, default now())`
* **posts:**
    * `post_id (UUID, PK)`
    * `user_id (UUID, FK references auth.users.id)`
    * `original_input (TEXT)`
    * `image_url (TEXT, nullable)`: URL to image in Supabase Storage.
    * `status (VARCHAR, CHECK(status IN ('draft', 'scheduled', 'published', 'error')), NOT NULL)`
    * `scheduled_at (TIMESTAMPTZ, nullable)`
    * `created_at (TIMESTAMPTZ, default now())`
    * `updated_at (TIMESTAMPTZ, default now())`
* **generated_content:**
    * `content_id (UUID, PK)`
    * `post_id (UUID, FK references posts.post_id ON DELETE CASCADE)`
    * `platform (VARCHAR, CHECK(platform IN ('linkedin', 'twitter')), NOT NULL)`
    * `generated_text (TEXT, NOT NULL)`
    * `created_at (TIMESTAMPTZ, default now())`
    * *(Constraint: UNIQUE(post_id, platform))*
* **social_connections:** (Stores OAuth tokens)
    * `connection_id (UUID, PK)`
    * `user_id (UUID, FK references auth.users.id)`
    * `platform (VARCHAR, CHECK(platform IN ('linkedin', 'twitter')), NOT NULL)`
    * `access_token (TEXT, NOT NULL)`: Should be encrypted.
    * `refresh_token (TEXT, nullable)`: Should be encrypted.
    * `expires_at (TIMESTAMPTZ, nullable)`
    * `scopes (TEXT)`: Comma-separated list of granted scopes.
    * `external_user_id (TEXT)`: User ID on the external platform.
    * `created_at (TIMESTAMPTZ, default now())`
    * `updated_at (TIMESTAMPTZ, default now())`
    * *(Constraint: UNIQUE(user_id, platform))*
* **analytics_snapshots:** (Stores periodic fetches of analytics data)
    * `snapshot_id (UUID, PK)`
    * `post_id (UUID, FK references posts.post_id ON DELETE CASCADE)`
    * `platform (VARCHAR, CHECK(platform IN ('linkedin', 'twitter')), NOT NULL)`
    * `fetched_at (TIMESTAMPTZ, default now())`
    * `views (INTEGER, nullable)`
    * `likes (INTEGER, nullable)`
    * `comments (INTEGER, nullable)`
    * `shares (INTEGER, nullable)`
    * `clicks (INTEGER, nullable)`
    * *(Consider indexing post_id, platform, fetched_at)*

*(Note: Encryption for sensitive data like access tokens needs to be handled, possibly application-side before saving to Supabase or using database-level encryption if available/suitable.)*
