# DoNotMakeMyTrip – AI Airline Assistant

An interactive **AI-powered airline booking assistant** that behaves like a smart travel agent. This project demonstrates how to build a **task-oriented, tool-using LLM application** with real-world APIs, multimodal outputs (text, image, audio), and a web-based UI.

> **Note:** This project intentionally uses **LLM-driven decision making with developer-controlled orchestration**. It is **not a fully agentic AI system**.

---

## What the App Does

The assistant can:
- Answer questions about **live flight ticket prices** using the **Amadeus API (sandbox)**
- Ask clarifying follow-up questions (origin, destination, dates)
- Book flights (simulated) and generate:
  - A **text booking confirmation** with a fake PNR
  - A **boarding-pass style image**
- Generate:
  - A **company logo** for *DoNotMakeMyTrip*
  - A **photo-realistic destination image** for the travel city
- Speak every response using **Text-to-Speech (TTS)**
- Provide everything through a **Gradio web interface** (chat + image + audio)

---

## Architecture Overview

This project follows a **model-in-the-loop** design:

- **Python controls the flow**
- **The LLM makes decisions**, such as:
  - Whether a tool should be called
  - Which tool to call
  - What arguments to pass

The model does **not** plan multiple steps or manage execution autonomously.

```
User → Gradio UI → Python Orchestrator
                     ↓
              LLM (Tool Decision)
                     ↓
            External APIs / Logic
                     ↓
              LLM (Final Reply)
                     ↓
                UI + Audio
```

---

## Technologies Used

### Large Language Models (LLMs)
- OpenAI Chat Completions API
- Tool calling (`tool_choice="auto"`)
- System prompts and structured outputs
- Two-step tool execution pattern

### External APIs
- **Amadeus Self-Service API (Sandbox)**
  - OAuth2 client_credentials flow
  - Flight offers (`/v2/shopping/flight-offers`)
  - Locations & airlines reference data

### Multimodal AI
- **Image Generation**
  - Company logo (vector-style branding)
  - Destination travel images (photo-realistic)
  - Boarding-pass mockups (PIL)
- **Audio**
  - Text-to-Speech (OpenAI TTS)
  - MP3 playback via Gradio

### Frontend / UI
- Gradio Blocks
- Chatbot interface
- Dynamic image panel
- Audio autoplay
- Persistent conversation state

---

## Key Features in Detail

### LLM Tool Calling
The LLM decides when to invoke:
- `get_live_ticket_prices`
- `book_flight`

Python executes the tool and returns results back to the model for natural-language generation.

### Live Flight Pricing
- City names are resolved to IATA codes
- Prices are fetched in real time from Amadeus
- The top-ranked flight offer is selected and summarized

### Booking Simulation
- Generates a fake PNR
- Creates structured booking data
- Renders a boarding-pass style image

### Visual Generation
- Logo generation at app startup
- Destination image based on travel city
- Boarding pass replaces destination image after booking

### Text-to-Speech
- Every assistant response is converted into speech
- Audio autoplays in the UI

---

## Project Structure

```
.
├── app.py              # Main Gradio application
├── requirements.txt    # Python dependencies
├── README.md           # Project documentation
```

---

## Environment Variables

This project requires API credentials. Set them as environment variables:

```bash
OPENAI_API_KEY=your_openai_key
AMADEUS_CLIENT_ID=your_amadeus_id
AMADEUS_CLIENT_SECRET=your_amadeus_secret
```

When deploying on **Hugging Face Spaces**, use **Settings → Secrets**.

---

##  Running Locally

```bash
pip install -r requirements.txt
python app.py
```

Then open the Gradio URL shown in the terminal.

---

## Deployment

This app is suitable for **free deployment on Hugging Face Spaces** using:
- Gradio SDK
- CPU runtime

> External API usage (OpenAI, Amadeus) may incur costs.

---

## Design Choice: Why This Is Not Agentic AI

This project intentionally avoids a fully agentic architecture:

- No autonomous planning loops
- No self-reflection or retries
- No goal-based execution

Instead, it demonstrates **safe, predictable, production-aligned LLM usage**, which is often preferred in real-world systems.

---

## What This Project Demonstrates

- Practical **LLM orchestration and tool usage**
- Real-world **API integration**
- **Multimodal AI pipelines** (text, image, audio)
- End-to-end ownership from backend logic to UI
- Continuous learning and experimentation with **LLMs**

---

## Disclaimer

- Flight bookings are **simulated**
- Prices come from the **Amadeus sandbox environment**
- PNRs and boarding passes are **not real**

---

## Author

**Kashif Moin**  
AI & Data Enthusiast | Continuously learning and working with LLMs  

GitHub: https://github.com/KashifMoin1410

---

If you find this project interesting, feel free to star the repo or reach out!

