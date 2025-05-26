Synergy o4‑mini Agents

A single‑file Python demo that spins up six autonomous agents using an internal "o4‑mini" cognitive model, a tiny LSTM for state memory, Bayesian updates, partial Monte‑Carlo Tree Search, a web‑navigation loop, and an optional Gmail integration for sending real e‑mail.

The built‑in Flask dashboard lets you watch reward curves, KL‑divergence, 9‑state cognitive distributions, and intra‑agent buddy chatter in real‑time.

## Features

 ✔ 

 Module 

 Notes 

 ✔ 

 o4‑mini cognitive model 

Deterministic snippet‑based responses plus LSTM memory – swappable for a larger LLM later

 ✔ 

 Partial MCTS reward loop 

Randomized rollout / reward accumulation per agent

 ✔ 

 9‑Dim Bayesian emotional distribution 

 CURIOUS … HUMOR with KL tracking

 ✔ 

 Real Gmail API send 

Authorise once → token.json cached

 ✔ 

 Ngrok tunnel (optional) 

Set NGROK_AUTH_TOKEN ENV var

 ✔ 

 Zero‑dependency dashboard 

Charts with Chart.js and a Vis‑Network nav‑map

 ✔ 

 MITM‑safe shutdown 

 curl -X POST /shutdown

## Quick Start

# 1 – Clone & install
pip install -r requirements.txt  # see below

# 2 – Put your Google client‑secret here
cp ~/Downloads/credentials.json ./credentials.json

# 3 – Run
python synergy_o4mini_real_gmail.py

First launch opens a browser page for Google OAuth; afterwards a token.json keeps refresh‑tokens.

Visit http://127.0.0.1:5002/dashboard (port auto‑increments) to watch the agents.

## Prerequisites

Python 3.8+

Gmail API credentials – create an OAuth 2.0 Desktop client in Google Cloud ⇒ download credentials.json.

Packages:

flask flask-socketio requests nest_asyncio torch bs4 pyngrok
chart.js vis-network
google-api-python-client google-auth-httplib2 google-auth-oauthlib

(pip install -r requirements.txt covers all of the above)

## Environment Variables

 Variable 

 Purpose 

 NGROK_AUTH_TOKEN 

(optional) create a public HTTPS tunnel

## Configuration

Drop credentials.json in the project root.  The first run stores token.json automatically.

## Usage Patterns

### Add a navigation task

curl -X POST http://localhost:5002/add-task \
     -H 'Content-Type: application/json' \
     -d '{"type":"navigate","content":"https://wikipedia.org"}'

### Send a real email
From the dashboard Send Email Task panel, fill in To / Subject / Body (link & attachment text are optional) and press Send Email.

Behind the scenes the agent enqueues a send_email task → _send_real_email_gmail() builds a text/plain message and fires the Gmail API.

## Extending

Replace produce_deep_buddy_msg with calls to an external LLM for richer dialogue.

Swap the LSTM‐based reward model with a transformer.

Add MIME multipart handling in _send_real_email_gmail() for binary attachments.

Pull‑requests & issues are welcome!

## License

Apache License 2.0 – see LICENSE for details.
