WorthTheTrip — Product Dataflow & Page Specifications

<table><tr>
<td><img src="WTT_Logo.jpeg" alt="WorthTheTrip logo" width="300" /></td>
<td><img src="workflow_gif.gif" alt="Demo hero animation" width="600" /></td>
</tr></table>

Purpose
-------
WorthTheTrip prevents unpaid, inefficient site visits by helping homeowners (clients) and skilled workers (labor) agree on fair pricing before anyone travels. 

**One visit, one job** 

Social Impact
------------------------------------

Unpaid site visits cost workers time, fuel, and income. WorthTheTrip removes uncertainty so effort is never wasted.

Documentation
------------------------------------
Figma: https://www.figma.com/board/S8ppwbijS37r7dXQEnhdbz/MASS-Hackathon2026?node-id=15-30&t=3WTbzMFeqsU5zafZ-0

Slides: https://www.figma.com/deck/MatovVTi3zcOcRje0HgKkW/worthTheTrip-Slides?node-id=1-439&t=4tmdISqwPJHpobLh-1


Architecture & Components
-------------------------
This project is split into three main components. Each component has its own repository and responsibilities outlined below.

1. Frontend

- Purpose: The user-facing application where all interaction happens — from browsing jobs to managing offers and profiles.
- Main responsibilities:
	- User authentication and profile management
	- Creating and editing job posts (description, location, images, videos)
	- Browsing jobs in list view and on an interactive Google Map
	- Filtering jobs by price, location, name, skills, and status (open, reserved, closed)
	- Sending and receiving offers
	- Notifications system (new offers, job updates)
	- Job lifecycle actions (reserve, close, accept completion)
- Tech stack: React, TypeScript, Vite, Google Maps API, REST API integration, modern component-based UI architecture
- Repository: https://github.com/MASS-Masters-Applying-Social-Solutions/WTT-Frontend

2. AI Service

- Purpose: Generates a price estimate for a job based on text and images.
- Main responsibilities:
	- Accepts job description, uploaded images, and address
	- Based on the job title, images and description. The AI agent looks up the internet and collects information from various sources from the web. The sources include various estimates of the job. AI agent smartly provide a rough minimum estimate of the costs.
	- Used during job creation to suggest a price to the user
- Core ideas: multimodal input (text + images), price estimation based on content, simple API interface for frontend/backend
- Repository: https://github.com/MASS-Masters-Applying-Social-Solutions/WTT-Backend-AI

3. Backend API

- Purpose: Core system that handles data, business logic, and permissions.
- Main responsibilities:
	- User creation, update, and profile management
	- Job CRUD (create, read, update, delete)
	- Offer system (send offer, accept offer, reject offer)
	- Job state management (open, reserved, closed)
	- Notifications (new offers, status changes, actions required)
	- Filtering and searching jobs (price, location, name, skills, status)
	- Integrating with the AI service for price estimation
	- Storing and serving images and videos (via external storage like Cloudinary)
- Tech stack: Node.js, REST API (Vercel serverless), Prisma ORM, relational database, cloud storage for media
- Repository: https://github.com/MASS-Masters-Applying-Social-Solutions/WTT-Backend

Core Product Flow (summary)
---------------------------
1. Client posts a job with clear details and photos.
2. AI suggests a fair market estimate from the job description and images.
3. Workers review the job, price, and media — then accept or counter.
4. Contact details unlock only after both sides agree. One visit. One job.

AI Pricing (Dataflow)
---------------------
- Input: Job title, description, images, pinned location, optional category/tags.
- Processing: AI model infers scope, materials, travel, local market rates and generates a recommended price range and single suggested price.
- Output: Suggested price and short rationale displayed on job card and job detail. Helper copy explains purpose: fairness & reducing wasted trips.

Dataflow — Event Sequence
-------------------------
1. Client creates job -> job saved (status: Open) -> AI estimate generated and attached.
2. Job appears on Browse and Map with AI price and media.
3. Worker views job detail -> can Accept, Counter, or Reject.
4. If worker Accepts (or parties agree on counter): status moves to Reserved/Confirmed, contact info unlocks for both sides.
5. After job completion: mark Completed; feedback/ratings optional.


