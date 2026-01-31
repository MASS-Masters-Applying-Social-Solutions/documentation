WorthTheTrip — Product Dataflow & Page Specifications

<table><tr>
<td><img src="WTT_Logo.jpeg" alt="WorthTheTrip logo" width="120" /></td>
<td><img src="workflow_gif.gif" alt="Demo hero animation" width="240" /></td>
</tr></table>

Purpose
-------
WorthTheTrip prevents unpaid, inefficient site visits by helping homeowners (clients) and skilled workers (labor) agree on fair pricing before anyone travels. This README documents the public/entry pages (pre-login), core UX flows, page-level content, microcopy guidance, architecture components, and the dataflow that makes **one visit, one job** possible.

Social Impact
------------------------------------

Unpaid site visits cost workers time, fuel, and income. WorthTheTrip removes uncertainty so effort is never wasted.

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
	- Processes text and images to estimate job cost (multimodal)
	- Returns a structured response (e.g. parts with prices like $150)
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

Accessibility & Trust
---------------------
- Use clear, high-contrast labels and large tappable targets for mobile.
- Explain AI pricing plainly; show a short rationale and allow counteroffers.
- Show social proof and simple verification steps to build trust (profile completeness, reviews).

Design Rationales — Why this works
----------------------------------
- Reduce decision friction: show price and media up-front so workers can decide without unnecessary clicks.
- Frame AI as fairness: recommended pricing prevents lowball visits and supports worker income.
- Unlock contact only after agreement: reduces spam and unpaid visits.

Next steps / Implementation notes
---------------------------------
- Wireframe each page using the content above.
- Define the API endpoints for job creation, AI pricing, job listing, accept/counter flows, and contact unlocking.
- Prototype the AI pricing model with sample dataset and iterate on transparency microcopy.

Contact
-------
Product & design: WorthTheTrip documentation

Purpose
-------
WorthTheTrip prevents unpaid, inefficient site visits by helping homeowners (clients) and skilled workers (labour) agree on fair pricing before anyone travels. This README documents the public/entry pages (pre-login), core UX flows, page-level content, microcopy guidance, and the dataflow that makes **one visit, one job** possible.

Social Impact
------------------------------------


Dataflow — Event Sequence
-------------------------
1. Client creates job -> job saved (status: Open) -> AI estimate generated and attached.
2. Job appears on Browse and Map with AI price and media.
3. Worker views job detail -> can Accept, Counter, or Reject.
4. If worker Accepts (or parties agree on counter): status moves to Reserved/Confirmed, contact info unlocks for both sides.
5. After job completion: mark Completed; feedback/ratings optional.
