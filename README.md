from flask import Flask, request, jsonify
import openai

app = Flask(__name__)

# OpenAI API Key
openai.api_key = "YOUR_OPENAI_API_KEY"

@app.route('/chat', methods=['POST'])
def chat():
    user_message = request.json.get('message')
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "user", "content": user_message}]
    )
    ai_reply = response['choices'][0]['message']['content']
    return jsonify({"reply": ai_reply})

if __name__ == '__main__':
    app.run()
