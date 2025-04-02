# DeepLearning 
Storytelling-Application
# 🧠 Storytelling Model Card

This is the model card of a 🤗 Transformers-based storytelling application that uses pretrained models to convert an image into a descriptive caption, generate a children's story from that caption, and provide audio narration using TTS (Text-to-Speech).

---

## Developed by
Eason Liu  
GitHub: [EasonLiu918](https://github.com/EasonLiu918)

---

## Model Type
Multimodal pipeline using:
- Vision-to-Text (Image Captioning)
- Text-to-Text (Story Generation)
- Text-to-Speech (TTS)

---

## Language(s)
- English (en)

---

## License
Open-source use only, for educational or non-commercial use.

---

## Finetuned from
- `Salesforce/blip-image-captioning-base`
- `facebook/opt-350m`
- TTS using `gTTS` (Google Text-to-Speech)

---

## Model Sources
- Hugging Face Models:
  - [Salesforce/blip-image-captioning-base](https://huggingface.co/Salesforce/blip-image-captioning-base)
  - [facebook/opt-350m](https://huggingface.co/facebook/opt-350m)
- TTS: [gTTS](https://pypi.org/project/gTTS/)

---

## Uses

### Direct Use
- Upload image → Caption → Story → Audio
- Children's storytelling, creativity apps, accessibility features

### Out-of-Scope Use
- Real-time applications
- Commercial deployment without content moderation
- Generation of offensive or misleading content

---

## Bias, Risks, and Limitations
- Model output may reflect biases from pretraining data.
- Not guaranteed to be appropriate for all ages without filtering.
- Language generation may contain inaccuracies.

---

## Recommendations
- Manually review generated stories before sharing.
- Do not rely on generated content for facts or critical decision-making.

---

## How to Get Started

```python
from transformers import pipeline
from gtts import gTTS
from PIL import Image

image_to_text = pipeline("image-to-text", model="Salesforce/blip-image-captioning-base")
story_gen = pipeline("text-generation", model="facebook/opt-350m")

caption = image_to_text("your_image.jpg")[0]['generated_text']
prompt = f"Write a magical story about: {caption}"
story = story_gen(prompt, max_length=300, do_sample=True)[0]['generated_text']

tts = gTTS(story)
tts.save("story.mp3")
