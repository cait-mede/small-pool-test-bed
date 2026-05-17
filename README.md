# Small Pool Test Bed

Test program for verifying that microservices can be called and respond with data.

## Microservices Under Test

1. **rating-service** - FastAPI service for managing ratings
   - Port: 8000
   - Endpoints: POST/GET/DELETE /ratings

2. **ai-prompt-service** - Express.js service for AI text/image generation
   - Port: 3000
   - Endpoint: POST /generate

3. **progress-service** - FastAPI service for tracking user reading progress
   - Port: 5003
   - Endpoint: GET /progress

## How to Run

### Prerequisites

1. Install dependencies for this test program:
```bash
pip install -r requirements.txt
```

2. Ensure each microservice is running:

#### Rating Service
```bash
cd ../rating-service
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

#### AI Prompt Service
```bash
cd ../ai-prompt-service
npm install
npm start  # Runs on port 3000
```

#### Progress Service
```bash
cd ../progress-service
pip install -r requirements.txt
python main.py   # Runs on port 5003
```

### Running the Tests

```bash
python test_microservices.py
```

## What the Test Program Does

The test program demonstrates:

- ✓ **Programmatic requests**: Test program makes HTTP requests to each service
- ✓ **Microservice responses**: Each service responds with JSON data
- ✓ **Programmatic data reception**: Test program receives and validates responses
- ✓ **Decoupled communication**: Services communicate via REST HTTP API, NOT direct function calls
- ✓ **Individual verification**: Each service is tested independently with its own endpoint tests

## Test Coverage

### Rating Service Tests
- POST /ratings - Create/update a rating
- GET /ratings - Retrieve ratings for an entity
- DELETE /ratings - Delete a rating

### AI Prompt Service Tests
- POST /generate - Generate text response
- POST /generate - Generate image response

### Progress Service
- GET /progress – Retrieve reading progress for a user/book pair

## Example Output

Status Code: 200
Raw Response: {"userId":"u123","bookId":"b456","currentPage":87,"percentageComplete":42}
Parsed JSON: {'userId': 'u123', 'bookId': 'b456', 'currentPage': 87, 'percentageComplete': 42}

progress-service: ✓ PASSED

============================================================
  TESTING RATING-SERVICE
============================================================

Test 1: Upserting a rating...
  POST http://localhost:8000/ratings
  Request: {
    "app_id": "book-club",
    "entity_id": "book-123",
    "user_id": "user-456",
    "rating": 5,
    "comment": "Excellent book!"
  }
  Status Code: 200
  Response: {'status': 'upserted'}
  ✓ PASSED
``` 
