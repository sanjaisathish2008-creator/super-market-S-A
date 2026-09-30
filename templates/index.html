import os
from flask import Flask, jsonify, render_template, request
from dotenv import load_dotenv
from google import genai
from google.genai import types
from chatbot_config import SYSTEM_PROMPT

load_dotenv()

app = Flask(__name__)

API_KEY = os.getenv("GEMINI_API_KEY")
MODEL = os.getenv("GEMINI_MODEL", "gemini-3.1-flash-lite")

if not API_KEY:
    raise RuntimeError("GEMINI_API_KEY is missing from .env")

client = genai.Client(api_key=API_KEY)


@app.get("/")
def index():
    return render_template("index.html")


@app.post("/api/chat")
def chat():
    data = request.get_json(silent=True) or {}
    message = str(data.get("message", "")).strip()
    history = data.get("history", [])

    if not message:
        return jsonify({"error": "Please enter a message."}), 400

    contents = []
    for item in history[-12:]:
        role = item.get("role")
        text = str(item.get("text", "")).strip()
        if role in ("user", "model") and text:
            contents.append(
                types.Content(
                    role=role,
                    parts=[types.Part.from_text(text=text)]
                )
            )

    contents.append(
        types.Content(
            role="user",
            parts=[types.Part.from_text(text=message)]
        )
    )

    try:
        response = client.models.generate_content(
            model=MODEL,
            contents=contents,
            config=types.GenerateContentConfig(
                system_instruction=SYSTEM_PROMPT,
                temperature=0.4,
                max_output_tokens=800,
            ),
        )
        return jsonify({"reply": (response.text or "").strip()})
    except Exception:
        return jsonify({"error": "Unable to process the request right now."}), 500


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=int(os.getenv("PORT", "5000")))
