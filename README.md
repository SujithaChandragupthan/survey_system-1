================================================================================
              SIMPLE SURVEY MANAGEMENT SYSTEM - README
================================================================================

A full-stack web application built using **Ruby on Rails (API-only)** as the backend 
and **React + Chakra UI** for the frontend. It manages Surveys, Survey Questions, 
User Assignments, and includes authentication with role-based access.

--------------------------------------------------------------------------------
TABLE OF CONTENTS
--------------------------------------------------------------------------------
1. Features
2. Tech Stack
3. User Roles
4. System Requirements
5. Running with Docker
6. API Endpoints
7. Running Tests
8. Project Structure
9. Notes

================================================================================
1. FEATURES
================================================================================
- User authentication
- Role-based access control (Admin, Manager, User)
- CRUD operations for surveys and survey questions
- Assign questions to users
- Users can respond to assigned questions
- Search/filter surveys using Ransack
- Responsive UI built with Chakra UI
- React Router for navigation
- PostgreSQL as the database
- Integrated unit testing using RSpec (backend) and React Testing Library (frontend)

================================================================================
2. TECH STACK
================================================================================
- Backend: Ruby on Rails API-only mode
- Frontend: React 18, Chakra UI, Axios, React Router
- Search: Ransack
- DB: PostgreSQL
- Containerization: Docker, Docker Compose
- Testing: RSpec (Rails), React Testing Library + Jest

================================================================================
3. USER ROLES
================================================================================
- Admin:
  • Full access to CRUD all resources
  • Assign questions to users

- Manager:
  • View all surveys
  • Create/update survey questions
  • Assign questions to users

- User:
  • Only view & respond to assigned questions

================================================================================
4. SYSTEM REQUIREMENTS
================================================================================
- Docker installed (https://www.docker.com)
- Docker Compose installed

================================================================================
5. RUNNING WITH DOCKER
================================================================================

1. Clone the repository:
   > git clone <your-repo-url>
   > cd SurveySystem

2. Start the entire stack (backend + PostgreSQL):
   > docker-compose up --build

   This will:
   - Start PostgreSQL container
   - Build and run the Rails backend

3. Open another terminal and run migrations & seed:
   > docker-compose exec web rails db:create db:migrate db:seed

4. Start React frontend (open in new terminal):
   > cd frontend
   > npm install
   > npm start

   Ensure frontend runs on port 3001 (set in `package.json` or `.env` if required)

5. Access the app:
   Backend API:     http://localhost:3000/api/
   React Frontend:  http://localhost:3001

================================================================================
6. API ENDPOINTS (MAIN)
================================================================================
- Auth:
  • POST   /api/survey_user_models/login         -> Login user by username/password

- Survey Models:
  • GET    /api/survey_models
  • POST   /api/survey_models
  • PUT    /api/survey_models/:id
  • DELETE /api/survey_models/:id
  PATCH  /api/survey_models/:id

- Survey Questions:
  • GET    /api/survey_questions/survey/:id
  • POST   /api/survey_questions
  • PUT    /api/survey_questions/:id
  • DELETE /api/survey_questions/:id
  PATCH  /api/survey_questions/:id
  DELETE /api/survey_questions/removeBySurvey/:survey_id
  
- Survey UserModels:
- GET    /api/survey_user_models
  POST   /api/survey_user_models
  GET    /api/survey_user_models/:id
  PATCH  /api/survey_user_models/:id
  PUT    /api/survey_user_models/:id
  DELETE /api/survey_user_models/:id
- Role Based Fetch:
  • GET    /api/survey_models/role?username=:username
 
================================================================================
7. RUNNING TESTS
================================================================================

▶ Rails Backend (RSpec)

> docker-compose exec web rspec

▶ React Frontend

> cd frontend
> npm test

================================================================================
8. PROJECT STRUCTURE
================================================================================

/backend
  ├── app/
  │   ├── controllers/api/
  │   ├── models/
  ├── config/
  ├── spec/
  │   ├── models/
  │   ├── controllers/
  |   ├── routing/
  └── Dockerfile
  └── docker-compose.yml

/frontend
  ├── src
  |   ├── components
  │   |   ├── Pages/
  │   |   ├── context/
  │   |   ├── Question/ 
  │   |   ├── Survey/
  │   └── App.js
  └── package.json

================================================================================
9. NOTES
================================================================================

• Admin credentials can be found in `db/seeds.rb` if seeded.
• Survey name is used as a reference key in navigation to fetch questions.
• The system gracefully handles unauthorized access with JSON error responses.
• RSpec test coverage includes models and controllers.
• Chakra UI is used for responsive and accessible UI components.

================================================================================
