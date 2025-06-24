+---------------------+ +--------------------------+ +----------------------+
| Service Provider UI | <-------> | | <-------> | External APIs |
| (Astro, Netlify) | | Serverless Backend (APIs)| | - LLM (Google Gemini)|
+---------------------+ | (Netlify Functions - | | - GitHub |
| Node.js) | | - Email Service |
+---------------------+ | | +----------------------+
| Admin UI | <-------> | |
| (Astro, Netlify) | +--------------------------+
| (Client/Repo Setup) | |
+---------------------+ |
v
+---------------------+
| Data Storage |
| (Supabase NoSQL - |
| Client Configs, |
| Users) |
+---------------------+
