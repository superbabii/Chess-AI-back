# Chess Evaluation and AI Chat API

This project provides an API for evaluating chess positions using the LCZero engine and interacting with OpenAI's GPT-based LLM for chess-related queries.

## Features

1. **Chess Evaluation**: Evaluate a chess position provided in FEN format, and get the best move suggestion with an evaluation score.
2. **AI Chess Chat**: Interact with a GPT-4-based language model for chess-related questions or descriptions of FEN positions.

---

## Installation and Setup

### Prerequisites

1. Python 3.8+
2. Flask
3. Flask-CORS
4. LCZero backend library
5. OpenAI Python SDK

### Clone Repository
```bash
git clone https://github.com/superbabii/Chess-AI-back
cd Chess-AI-back
```

### Install Dependencies
```bash
pip install flask flask-cors openai
```

### Configure LCZero Weights
- Download the required LCZero weights file (e.g., `744706.pb.gz`).
- Place it in a folder named `weights` in the project directory.

### OpenAI API Key
- Set your OpenAI API key as an environment variable.
```bash
export OPENAI_API_KEY='your_openai_api_key_here'
```

---

## API Endpoints

### 1. `/evaluate`

#### Method: POST

**Description:** Evaluate a chess position given in FEN format.

#### Request
```json
{
    "fen": "<FEN string>"
}
```

#### Response
```json
{
    "evaluation": <float>,
    "best_move": {
        "from": "<square>",
        "to": "<square>"
    }
}
```

#### Errors
- `400`: FEN not provided.
- `500`: Internal evaluation error.

#### Example
```bash
curl -X POST http://127.0.0.1:8000/evaluate \
-H "Content-Type: application/json" \
-d '{"fen": "rnbqkb1r/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"}'
```

### 2. `/llm_chat`

#### Method: POST

**Description:** Interact with a GPT-based model to ask chess-related questions or describe positions.

#### Request
```json
{
    "query": "<user question>",
    "fen": "<FEN string>"
}
```
**Note:** Either `query` or `fen` must be provided.

#### Response
```json
{
    "response": "<chatbot response>"
}
```

#### Errors
- `400`: Invalid input (neither `query` nor `fen` provided).
- `500`: LLM processing error.

#### Example
```bash
curl -X POST http://127.0.0.1:8000/llm_chat \
-H "Content-Type: application/json" \
-d '{"query": "What is the best opening for white?"}'
```

---

## Development Notes

### Running the API Locally

Start the Flask application:
```bash
python app.py
```

Access the API at `http://127.0.0.1:8000/`

### Testing with CURL
Use `curl` or tools like Postman to test API endpoints.

### Debugging
Enable Flask debug mode by setting `FLASK_ENV`:
```bash
export FLASK_ENV=development
```

---

## Folder Structure

```
.
├── app.py               # Main Flask app
├── weights/             # Directory for LCZero weights
│   └── 744706.pb.gz
├── requirements.txt     # Python dependencies
└── README.md            # Project documentation
```

---

## Future Enhancements

1. Add user authentication.
2. Implement more advanced evaluation features like multi-depth analysis.
3. Enhance LLM responses with real-time chess databases.
4. Expand support for multi-player and game tracking.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.

