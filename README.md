Overview
This repository implements a WhatsApp chatbot using Flask and Meta's WhatsApp Business API, powered by OpenAI's Assistants API. Designed specifically for assisting guests at a Paris Airbnb, the bot handles inquiries by retrieving knowledge from an FAQ PDF (e.g., check-in details, amenities, local tips). It processes incoming messages via webhooks, generates intelligent responses, and sends replies seamlessly. Includes webhook verification, signature validation, and conversation threading for persistent chats.
Perfect for property managers or hosts wanting automated, AI-driven guest support on WhatsApp.
Features

Webhook Integration: Handles incoming WhatsApp messages with verification and HMAC signature checks.
AI-Powered Responses: Uses OpenAI GPT-4 with Assistants API and file-based retrieval from airbnb-faq.pdf for contextual answers.
Message Formatting: Adapts responses for WhatsApp (e.g., bold text with *, removes markdown artifacts).
Conversation Persistence: Maintains chat threads per user via shelve database.
Error Handling: Manages API timeouts, invalid payloads, and status updates (sent/delivered/read).
Quickstarts: Example scripts for setting up OpenAI assistants and WhatsApp API.

Technologies

Framework: Flask (web server and routes)
API Integrations: Meta WhatsApp Business API (Graph API), OpenAI Assistants API
Language: Python 3.x
Other: python-dotenv (env vars), requests/aiohttp (HTTP), shelve (thread storage)

Installation

Clone the repository:textgit clone https://github.com/Shreyaaaa010102/whatsapp-chatbot.git
cd whatsapp-chatbot
Create a virtual environment (recommended):textpython -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
Install dependencies:textpip install -r requirements.txt
Set up environment variables in a .env file (based on config.py):textACCESS_TOKEN=your_whatsapp_access_token
YOUR_PHONE_NUMBER=your_phone_number
APP_ID=your_app_id
APP_SECRET=your_app_secret
RECIPIENT_WAID=recipient_whatsapp_id
VERSION=v18.0  # WhatsApp API version
PHONE_NUMBER_ID=your_phone_number_id
VERIFY_TOKEN=your_webhook_verify_token
OPENAI_API_KEY=your_openai_api_key  # Add this for OpenAI
Obtain WhatsApp credentials from Meta for Developers.
Upload data/airbnb-faq.pdf (or your FAQ file) and note its file ID in openai_service.py.


Usage

Run the Flask app:textpython run.pyThe server starts on http://0.0.0.0:8000.
Configure Webhook:
In your WhatsApp Business app on Meta Developers, set the webhook URL to https://your-domain.com/webhook (use ngrok for local testing: ngrok http 8000).
Verify with the VERIFY_TOKEN from your .env.

Test the Bot:
Send a message to your WhatsApp Business number.
The bot will respond with AI-generated answers based on the FAQ (e.g., "What time is check-in?").


Example Flow

Incoming message: "Hi, what's the WiFi password?"
Bot: Retrieves from FAQ → "The WiFi password is 'ParisGuest2023'. Connect to 'AirbnbParisWiFi'."

Customization

Update assistant instructions in openai_service.py (e.g., "You're a helpful assistant for our Paris Airbnb...").
Modify process_whatsapp_message in whatsapp_utils.py for custom logic.

Project Structure
textwhatsapp-chatbot/
├── __init__.py          # Flask app factory (create_app)
├── app/                 # Wait, no subdir—flat structure
├── assistants_quickstart.py  # OpenAI setup example
├── config.py            # App config loader
├── gitignore.txt        # Git ignore rules
├── openai_service.py    # OpenAI integration (threads, runs, responses)
├── requirements.txt     # Dependencies
├── run.py               # Entry point to start the app
├── security.py          # Signature validation (assumed)
├── views.py             # Flask routes (webhook GET/POST)
├── whatsapp_quickstart.py # WhatsApp API example
└── whatsapp_utils.py    # Message sending, processing, formatting
Contributing

Fork the repo and submit a PR.
Add new tools to the OpenAI assistant (e.g., function calling).
Improve error logging or add unit tests.
Follow PEP 8 for code style.

License
MIT License.
Contact
Shreyaaaa010102 - Open issues for bugs or features!
