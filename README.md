# Smart Medicine Inventory Device (MediMate)

A small web app for keeping track of medicines at home. You can log what you have, where it's stored and how much is left, set reminder alarms for doses, and ask a simple built-in chatbot (MediMate) for basic help.

The full project write-up is in `Smart_Medicine_Storage_Device.pdf`.

## Features

- **Medicine inventory:** add medicines with name, quantity, description and storage location; search by name or description; edit quantities or remove entries
- **Reminder alarms:** set a date, time and message, repeating hourly, daily, weekly or monthly
- **MediMate chatbot:** a small intent-classification chatbot trained on `intents.json` (greetings, general health tips and so on)

## How the chatbot works

`train.py` tokenizes and lemmatizes the example phrases with NLTK, turns them into bag-of-words vectors and trains a small Keras network (128 → 64 → softmax, with dropout, SGD with Nesterov momentum). `chatbot.py` loads the trained model in a Flask app, classifies each message and replies with one of the answers for the predicted intent.

## Tech stack

- Python, Flask
- TensorFlow / Keras, NLTK, NumPy
- HTML, CSS, vanilla JavaScript

## Running it

```bash
pip install flask tensorflow nltk numpy
python train.py      # optional, retrains chatbot_model.h5
python chatbot.py    # then open http://127.0.0.1:5000
```

## Files

| File | What it is |
|---|---|
| `chatbot.py` | Flask server and chatbot inference |
| `train.py` | Trains the intent classifier |
| `intents.json` | Training phrases and responses |
| `chatbot_model.h5`, `words.json`, `classes.json` | Trained model and vocabulary |
| `templates/`, `static/` | Frontend (inventory, reminders, chat UI) |
| `Smart_Medicine_Storage_Device.pdf` | Project report |
