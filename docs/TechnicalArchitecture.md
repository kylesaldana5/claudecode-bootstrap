# Technical Architecture Design: AI Blog Post Generator

**Version:** 1.0
**Date:** June 21, 2025
**Architect:** Sam

---

### 1. High-Level Architecture Overview

At a glance, the system will primarily consist of a modern web application frontend, a serverless backend handling the core logic, and integrations with external services. We now also clearly define a crucial **Admin role** responsible for system configuration.

- **User Interface (AI Blog Post Generator App - Service Provider View):** This is the web interface you (the service provider) will interact with for generating and publishing blog posts. It will be built using Astro and hosted on Netlify. It offers a streamlined view, abstracting away backend complexities.
- **User Interface (AI Blog Post Generator App - Admin View):** A separate or integrated view/functionality within the app for an Administrator. This role will handle the setup and management of client configurations, GitHub repository associations, and potentially service provider user accounts and API key management. This will likely be your role initially.
- **Serverless Backend (Netlify Functions):** This will be the "brain" of the application, acting as the API layer. It will handle requests from both the service provider and admin UIs, interact with the AI model, manage GitHub operations, and interface with the data storage. We'll use Netlify Functions for seamless integration with your existing Netlify hosting, implemented in **Node.js**.
- **External APIs:**
  - **Large Language Model (LLM) API:** Specifically **Google's Gemini API**, for AI-powered content generation.
  - **GitHub API:** Used to interact with client repositories (branching, committing, creating PRs).
  - **Email Notification Service:** For sending automated alerts _to the service provider_.
- **Data Storage:** **Supabase (Serverless NoSQL Database)** for client configurations and user data.
- **GitHub Repositories:** Both for the AI Blog Post Generator app's code and for your clients' Astro/Decap CMS websites.

---

### 2. Component Breakdown

This section details each major component within the architecture, outlining its purpose, key technologies, and responsibilities.

#### 2.1 User Interface (UI) Components

These are the web applications the users (Service Provider and Admin) will interact with.

- **Service Provider UI (Astro App):**

  - **Purpose:** The primary interface for the service provider to generate, edit, and publish blog posts. Designed for simplicity and efficiency.
  - **Technologies:** Astro (frontend framework), HTML, CSS, JavaScript/TypeScript.
  - **Hosting:** Netlify.
  - **Key Responsibilities:**
    - Displaying input fields for blog topics, keywords, length, and structure.
    - Rendering AI-generated content for review and editing.
    - Providing a "Publish" button.
    - Displaying success/error notifications for publication status (frontend alert for the service provider).
    - Secure service provider login form.

- **Admin UI (Astro App - potentially integrated or separate sections):**
  - **Purpose:** Interface for managing backend configurations that the service provider doesn't interact with directly. This includes client profiles, GitHub repository mappings, service provider user accounts, and API key management.
  - **Technologies:** Astro (frontend framework), HTML, CSS, JavaScript/TypeScript.
  - **Hosting:** Netlify (likely part of the same Astro app, but with restricted access).
  - **Key Responsibilities:**
    - Forms for creating/editing client profiles (brand voice, tone, industry).
    - Fields for associating client profiles with specific GitHub repository URLs.
    - User management for service provider accounts.
    - Interface for managing AI model and GitHub API keys (e.g., setting environment variables or interacting with a secret store).

#### 2.2 Backend Components

These are the server-side logic components responsible for processing requests, interacting with external APIs, and managing data.

- **Serverless Functions (Netlify Functions):**
  - **Purpose:** The core backend logic and API layer for the application. Each function will handle a specific task (e.g., generate content, publish to GitHub).
  - **Technologies:** **Node.js** (chosen for ecosystem cohesion and Netlify optimization), exposed via HTTP endpoints.
  - **Hosting:** Netlify (seamlessly deployed with the frontend).
  - **Key Responsibilities:**
    - **Authentication & Authorization:** Validating service provider and admin logins, ensuring only authorized users can perform actions.
    - **Client Context Resolver:** Based on the logged-in user, automatically retrieve and provide the correct client's pre-configured brand configuration and associated GitHub repository details from the Data Storage.
    - **AI Orchestrator:** Call **Google's Gemini API** with dynamic prompts incorporating client brand voice, topic, keywords, length, and structure. Handle API responses.
    - **GitHub Integrator:** Interact with the GitHub API to:
      - Create new branches.
      - Commit Markdown/MDX files and images.
      - Create Pull Requests.
      - Handle GitHub API rate limits and errors.
    - **Data Access Layer:** Interact with the Data Storage to read/write client configurations and user data.
    - **Error Handling & Notifications:** Catching backend errors and triggering email notifications _to the service provider_ for critical failures (e.g., publication failures). The frontend will handle alerting the service provider directly within the UI if something goes wrong.

#### 2.3 Data Storage

- **Purpose:** Persist client configurations (brand details, GitHub repo mappings), service provider user accounts, and potentially content drafts/history.
- **Chosen Technology:** **Supabase (Serverless NoSQL Database)**.
  - **Key Responsibilities:**
    - Storing client `id` mapped to brand voice, tone, industry, and GitHub `repo_url`.
    - Storing service provider `user_id` mapped to authentication credentials and associated client `id`.
    - (Optional, for future) Storing draft blog posts or publication history.

#### 2.4 External Services/APIs

- **Large Language Model (LLM) API:**
  - **Purpose:** Provide the core AI capability for generating blog post text.
  - **Provider:** **Google's Gemini API** (chosen for simplicity and security).
  - **Interaction:** Serverless Functions will make HTTP POST requests to the LLM API endpoints.
- **GitHub API:**
  - **Purpose:** Programmatically interact with client GitHub repositories to manage code and content.
  - **Interaction:** Serverless Functions will make authenticated HTTP requests using Personal Access Tokens (PATs) or GitHub Apps credentials.
- **Email Notification Service:**
  - **Purpose:** Send automated email alerts _to the service provider_ in case of publication failures or critical system errors. This will serve as the initial monitoring mechanism.
  - **Providers:** Choose the simplest possible option for sending basic notifications (e.g., a lightweight service or even a direct integration with a basic email API).
  - **Interaction:** Serverless Functions will trigger these email sends.

---

### 3. Data Flow and Interactions

This section describes the sequence of operations and data exchange between the different components of the system for key user flows.

#### 3.1 Service Provider Login Flow

1.  **Service Provider (UI):** Enters login credentials (e.g., username/password) into the Astro frontend.
2.  **Service Provider (UI) -> Serverless Function (Authentication):** Sends login request to a dedicated Netlify Function for authentication.
3.  **Serverless Function (Authentication) -> Data Storage (Supabase):** Verifies credentials against stored service provider user data in Supabase.
4.  **Data Storage (Supabase) -> Serverless Function (Authentication):** Returns authentication result and the `service_provider_id` (and potentially associated client ID(s) if applicable, or the ability to look them up).
5.  **Serverless Function (Authentication) -> Service Provider (UI):** Returns a secure token (e.g., JWT) to the frontend upon successful authentication.
6.  **Service Provider (UI):** Stores the token securely (e.g., in `localStorage` or `sessionStorage`) for subsequent authenticated requests.

#### 3.2 Blog Post Generation Flow

1.  **Service Provider (UI):** Submits the blog post request (topic, keywords, length, structure) to a Serverless Function. The UI implicitly passes the `service_provider_id` via the authentication token.
2.  **Service Provider (UI) -> Serverless Function (AI Orchestrator):** Sends the generation request.
3.  **Serverless Function (AI Orchestrator) -> Data Storage (Supabase):** Uses the `service_provider_id` to query Supabase for the associated client's pre-configured brand voice, tone, and other relevant settings (e.g., `client_id`, `repo_url`).
4.  **Data Storage (Supabase) -> Serverless Function (AI Orchestrator):** Returns client configuration data.
5.  **Serverless Function (AI Orchestrator) -> LLM API (Google Gemini):** Constructs a dynamic prompt using the input request and client configuration, then sends it to the Google Gemini API.
6.  **LLM API (Google Gemini) -> Serverless Function (AI Orchestrator):** Returns the AI-generated blog post content.
7.  **Serverless Function (AI Orchestrator) -> Service Provider (UI):** Sends the generated content back to the frontend for display and review.

#### 3.3 Blog Post Publication Flow

1.  **Service Provider (UI):** Clicks "Publish" on the reviewed blog post. The UI sends the content, relevant metadata, and implicitly the `service_provider_id`.
2.  **Service Provider (UI) -> Serverless Function (GitHub Integrator):** Sends the publication request.
3.  **Serverless Function (GitHub Integrator) -> Data Storage (Supabase):** Retrieves the associated client's GitHub `repo_url` based on the `service_provider_id` (if not already cached).
4.  **Data Storage (Supabase) -> Serverless Function (GitHub Integrator):** Returns the GitHub `repo_url`.
5.  **Serverless Function (GitHub Integrator) -> GitHub API:**
    - Creates a new branch for the blog post.
    - Formats the content into Markdown/MDX with front matter.
    - Commits the content file to `/src/content/blog/` in the new branch.
    - (If applicable) Commits associated image files to `src/assets/images/blog/`.
    - Creates a Pull Request (PR) from the new branch to the client's main branch.
6.  **GitHub API -> Serverless Function (GitHub Integrator):** Returns the status of the GitHub operations (success/failure, PR URL).
7.  **Serverless Function (GitHub Integrator) -> Service Provider (UI):** Sends a simple success/error notification back to the frontend.
8.  **Serverless Function (GitHub Integrator) -> Email Notification Service:** If the publication fails, triggers an email to the service provider (you).

#### 3.4 Admin Configuration Flow (for Admin UI)

1.  **Admin (UI):** Logs in securely (similar to Service Provider login, potentially with higher privileges).
2.  **Admin (UI) -> Serverless Function (Admin API):** Submits forms for creating/updating client profiles (brand voice, GitHub repo URL, etc.) or managing service provider users.
3.  **Serverless Function (Admin API) -> Data Storage (Supabase):** Writes/updates client configuration data and/or service provider user data in Supabase.
4.  **Data Storage (Supabase) -> Serverless Function (Admin API):** Confirms data persistence.
5.  **Serverless Function (Admin API) -> Admin (UI):** Returns success/error confirmation.

---

### 4. Key Technical Considerations

This section addresses important architectural decisions, design patterns, and cross-cutting concerns that will influence the development and operational aspects of the system.

#### 4.1 Authentication and Authorization Strategy

- **Service Provider Authentication:**
  - **Method:** Leverage Supabase's built-in authentication capabilities (e.g., email/password, potentially OAuth for Google if desired for simplicity). Supabase provides secure user management and token handling (JWTs).
  - **Flow:** Upon successful login, a JWT token is issued by Supabase, which the frontend will store. This token will be sent with all subsequent requests to Serverless Functions for authentication.
- **Authorization (Service Provider vs. Admin):**
  - **Method:** Implement role-based access control (RBAC). The JWT will contain `roles` or `permissions` claims (e.g., `service_provider`, `admin`).
  - **Enforcement:** Serverless Functions will inspect these claims to ensure that only authenticated and authorized users can access specific API endpoints (e.g., only `admin` can call client configuration management APIs).
- **GitHub API Authentication:**
  - **Method:** Use a GitHub App or a Personal Access Token (PAT) with appropriate fine-grained permissions. GitHub Apps are generally more secure and scalable for programmatic access across multiple repositories.
  - **Storage:** The GitHub App credentials or PAT will be securely stored as environment variables within Netlify, accessible only to the Serverless Functions.

#### 4.2 Data Storage Design (Supabase)

- **Schema:**
  - **`service_providers` table:** Stores user credentials (managed by Supabase Auth), `email`, `name`, and potentially `role` (e.g., 'service_provider', 'admin').
  - **`clients` table:** Stores `client_id`, `client_name`, `brand_voice_profile` (JSON or text), `industry_niche`, `github_repo_url`, `main_branch_name` (e.g., 'main', 'production'), and `service_provider_id` (foreign key linking to `service_providers`).
  - (Optional, for future) `blog_posts_drafts` table: To store drafts or publication history.
- **Security (Row Level Security):** Leverage Supabase's Row Level Security (RLS) policies to ensure that:
  - Service providers can only access data relevant to the clients they are associated with (if applicable).
  - Admin users have broader access.

#### 4.3 API Key and Secret Management

- All sensitive API keys (LLM, GitHub, Email Service) will be stored as **environment variables** in Netlify.
- For **increased security**, we will explicitly utilize **Netlify's built-in support for encrypted environment variables**. This provides a robust solution for protecting sensitive credentials.

#### 4.4 Error Handling and Observability

- **Frontend Error Handling:** Display user-friendly alerts (e.g., toasts, banners) for API failures or invalid inputs.
- **Backend Error Handling (Serverless Functions):**
  - Implement `try-catch` blocks for all external API calls (LLM, GitHub, Supabase).
  - Log detailed error messages (including request payloads, responses, stack traces) to Netlify Functions logs.
  - Specific error codes or messages will be returned to the frontend.
- **Logging:** Utilize Netlify's built-in logging capabilities. For more advanced monitoring, integrate with a third-party logging service (e.g., Datadog, Sentry, Logtail) if detailed analytics or alerting are needed beyond simple email notifications.
- **Monitoring (Initial):** Email notifications to the service provider (you) for critical failures (e.g., failed GitHub publication) will serve as the initial monitoring mechanism.

#### 4.5 Performance Optimizations

- **AI API Calls:**
  - Implement efficient prompt engineering to get desired results with fewer tokens, reducing cost and latency.
  - Consider caching mechanisms for repeated client configurations to avoid redundant database lookups.
- **Serverless Cold Starts:** While Netlify Functions generally have good cold start performance, for highly latency-sensitive operations, consider strategies like "warming" functions if necessary (though often not needed for typical web app usage).
- **Frontend Performance:** Optimize Astro build processes, lazy load components, and optimize images to ensure fast loading times for the UI.

#### 4.6 Continuous Integration/Continuous Deployment (CI/CD)

- **GitFlow/GitHub Flow:** Maintain the GitHub Flow strategy for version control, using feature branches and Pull Requests.
- **Automated Deployment:** Configure Netlify to automatically build and deploy changes to the production environment upon merges to the `main` branch of the AI Blog Post Generator app's GitHub repository.
- **Testing in CI:** Integrate unit, integration, and end-to-end tests into the CI pipeline to ensure code quality and prevent regressions before deployment.
