<h1>
  <span class="headline">Build a FastAPI Application Project</span>
  <span class="subhead">Step By Step Project Build</span>
</h1>

## Project Instructions

For your project, you will be building and testing an API using **Python**, **FastAPI**, and **React**, with optional testing using **Pytest**, and **HTTPX**. This project will give you the opportunity to build a complete API with full CRUD functionality with a React frontend, as well as write automated tests to ensure its reliability.

### **Choose Your Theme**

Start by choosing a theme or service that interests you. Consider building an API that aligns with sustainability, community impact, or any area you’re passionate about.

### **What You'll Learn:**

By completing this project, you’ll

- Build a modular, well-structured FastAPI application.

- Implement full CRUD (Create, Read, Update, Delete) operations with authorization restricting access to resources.
  
- Create a dynamic React frontend with RESTful routing.

Bonus:

- Write automated tests for your API endpoints using Pytest and HTTPX.

- Develop skills for building and testing real-world APIs.

### **Getting Started**

Follow the provided project outline and reference our in-class lesson materials to create a fullstack application with a fully functional API and thorough test coverage. This project is your chance to combine coding and testing skills into a valuable, portfolio-worthy application.

## 1. Initialize FastAPI Project

1. **Create a Python virtual environment and install dependencies:**

   ```bash
   pip install fastapi uvicorn sqlalchemy psycopg2-binary pydantic passlib bcrypt pyjwt
   pip install pytest starlette httpx
   ```

2. **Set Up Your Project Structure:**

Organize your app into folders:

```text
   /project
   ├── config/
   ├── controllers/
   ├── data/
   ├── dependencies/
   ├── models/
   ├── serializers/
   ├── tests/
   ├── database.py
   ├── main.py
   ├── seed.py
   ├── Pipfile
```

3. **Create a FastAPI App:**

   In `main.py`, initialize a FastAPI app and include routers:

```python
 from fastapi import FastAPI
 from routes import items

 app = FastAPI()

 app.include_router(items.router, prefix="/api")
```

---

## 2. Choose Your API Theme

Think about a topic you’re passionate about or interested in, such as:

- Personal Finance Manager: Track income, expenses, and budgets in various currencies, with features to provide savings tips based on global financial practices.
- Travel and Culture Explorer: Plan trips and store destination details, including local landmarks, cultural activities, and festivals, with options for different language preferences and country-specific travel recommendations.
- Global Recipes Database: Store and retrieve recipes from various cuisines around the world, with options to filter by dietary preferences or regional styles.
- Health and Wellness Tracker: Log workouts, meals, and wellness activities, with the ability to track health trends, tips, and customizable features like fasting schedules.
- International Events Planner: Organize and manage events, with customizable features for different regions, including language preferences, time zone adjustments, and event types.

Your API should support full CRUD operations:

| **HTTP Method** | **Endpoint**      | **Description**                | **Request Body**                                       | **Response**                                |
| --------------- | ----------------- | ------------------------------ | ------------------------------------------------------ | ------------------------------------------- |
| GET             | `/api/items`      | Retrieve all items             | None                                                   | JSON object with an array of all items      |
| POST            | `/api/items`      | Add a new item                 | `{ "id": int, "name": string, "description": string }` | JSON object with the newly created item     |
| GET             | `/api/items/{id}` | Retrieve a specific item by ID | None                                                   | JSON object with the item details           |
| PUT             | `/api/items/{id}` | Update an existing item        | `{ "name": string, "description": string }`            | JSON object with the updated item           |
| DELETE          | `/api/items/{id}` | Delete an item                 | None                                                   | JSON object confirming deletion or an error |

## 3. Implement Your FastAPI Application

### Define Models and Schemas

1. **Create your database models in `models/`**

   Define SQLAlchemy models for your items.

2. **Create named Pydantic schemas in `serializers/`:**

   Define validation schemas for request and response data.

### Implement the Routes

1. **Create routes in `controllers/`:**

   Implement the endpoints using FastAPI’s dependency injection and response models.

### Run the Server

Use `uvicorn` to start the server:

```bash
pipenv run uvicorn main:app --reload
```

Test your API manually using a tool like Postman or the FastAPI interactive docs at `http://127.0.0.1:8000/docs`.

## 4. Initialize your React frontend.

1. **Create a directory 'client' or 'frontend' adjacent to your FastAPI project directory.**

   ```bash
   mkdir client
   ```
2. **Create a new project with Vite.**

  ```bash
  npm create vite@latest my-react-app 
  cd my-react-app
  ```

3. **Select your Framework and Variant (these should be React and Javascript respectively).**

4. **Install dependencies.**
  
   ```bash
   npm install
   ```

5. **In your FastAPI application, add the port of your frontend server to the list of allowed origins inside of main.py**

   ```python
   app.add_middleware(
     CORSMiddleware,
       allow_origins=['http://localhost:5173', 'http://127.0.0.1:5173' ], # <-- Add frontend port URLs here.
       allow_credentials=True,
       allow_methods=['*'],
       allow_headers=['*']
     )
    ```

6. **Run your server.**

   ```bash
   npm run dev
   ```

### **Optional Bonus**
## 5. Writing Tests Using Pytest and HTTPX

1. **Create a `tests` Directory:**

   Store your test files in a `tests/` folder.

2. **Write Test Cases in `tests/test_items.py`:**

   Use `httpx.AsyncClient` to test API endpoints asynchronously.

3. **Write Additional Tests for Full CRUD Operations:**

   - Test creating an item (`POST /api/items`)
   - Test retrieving an item by ID (`GET /api/items/{id}`)
   - Test updating an item (`PUT /api/items/{id}`)
   - Test deleting an item (`DELETE /api/items/{id}`)

## 5. Run the Tests

Execute your tests using Pytest:

```bash
pipenv run pytest
```

You should see results indicating whether your API endpoints work as expected.
