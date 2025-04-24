# 📢 Voice-to-Image Generation with DALL·E

Transform your voice into AI-generated art. Speak a prompt → Get an image. This notebook connects **speech recognition** with **OpenAI’s DALL·E API** to visualize your words.

---

## 🚀 Features

- 🎤 Record your voice in real time  
- 📝 Transcribe it into text  
- 🎨 Generate images using OpenAI’s DALL·E  
- 🖼️ Display results inline

---

## 🧠 How It Works – Step by Step

### 1. **Record voice input**

Capture user audio via microphone using the `speech_recognition` library.

```python
import speech_recognition as sr

recognizer = sr.Recognizer()
with sr.Microphone() as source:
    print("Speak now...")
    audio = recognizer.listen(source)
```

📌 *This records your voice until you stop speaking.*

---

### 2. **Transcribe to text**

Convert audio to text using Google Web Speech API:

```python
prompt = recognizer.recognize_google(audio)
print(f"You said: {prompt}")
```

📌 *We now have a text prompt ready to send to the image generator!*

---

### 3. **Generate image with OpenAI**

Use the OpenAI API to generate an image from the prompt.

```python
import openai

openai.api_key = "your-api-key"

response = openai.Image.create(
    prompt=prompt,
    n=1,
    size="512x512"
)

image_url = response['data'][0]['url']
```

📌 *This step sends the text to DALL·E and retrieves an image URL.*

---

### 4. **Display the image**

Fetch and show the generated image using `PIL` and `IPython.display`.

```python
from PIL import Image
import requests
from IPython.display import display

image = Image.open(requests.get(image_url, stream=True).raw)
display(image)
```

📌 *Voilà! The generated image appears right in your notebook.*

---

## 🧪 Requirements

Install dependencies:

```bash
pip install openai speechrecognition pyaudio requests pillow
```

---

## 📁 Files

```plaintext
voice-to-image-generation-dalle/
├── voice-to-image-generation-dalle.ipynb
├── requirements.txt
├── README.md
└── assets/
```

---

## ▶️ Try It Yourself

1. Clone the repo  
2. Run the notebook  
3. Speak your dream scene!

---

## 🔐 Notes

- You need an [OpenAI API Key](https://platform.openai.com/account/api-keys)
- `pyaudio` may require additional system-specific installation
