# MediaRouter

MediaRouter is a notebook project that builds a simple multimodal generation agent. It takes a user prompt, classifies the request, and routes it to the right generation path: question answering, text-to-image, or text-to-video.

The project is implemented in [Build_a_Multi_Modal_Generation_Agent.ipynb](Build_a_Multi_Modal_Generation_Agent.ipynb).

## What It Does

- Generates images from text prompts with Stable Diffusion XL.
- Generates short videos from text prompts with a text-to-video diffusion model.
- Uses a language model to classify user prompts into `qa`, `image`, or `video`.
- Routes each prompt to the correct handler through a multimodal agent function.
- Provides a simple Gradio interface for interactive use.

## Main Components

- **Text-to-image pipeline**: Uses `stabilityai/stable-diffusion-xl-base-1.0` through Hugging Face Diffusers.
- **Text-to-video pipeline**: Uses `damo-vilab/text-to-video-ms-1.7b` through Hugging Face Diffusers.
- **Prompt classifier**: Uses `google/gemma-3-1b-it` to decide whether a prompt should produce text, an image, or a video.
- **Agent router**: Calls the appropriate generation function based on the classifier output.
- **Gradio app**: Exposes the agent through a small browser-based interface.

## Requirements

This project is designed for a Python notebook environment with GPU support. The diffusion models are large, so running on CPU will be slow and may not be practical.

Install the main dependencies:

```bash
pip install torch diffusers transformers huggingface_hub accelerate matplotlib pillow numpy gradio
```

Depending on your machine and CUDA version, you may need to install PyTorch using the official command from the PyTorch installation page.

## Hugging Face Access

Some models may require a Hugging Face account, accepted model terms, or an access token.

Do not hard-code tokens in the notebook. Use an environment variable instead:

```bash
export HF_TOKEN="your_token_here"
```

Then log in from Python:

```python
import os
from huggingface_hub import login

login(token=os.environ["HF_TOKEN"])
```

If a token was previously committed or shared, rotate it in your Hugging Face account settings.

## How To Run

1. Open `Build_a_Multi_Modal_Generation_Agent.ipynb` in Jupyter, VS Code, or Google Colab.
2. Install the required packages.
3. Log in to Hugging Face if needed.
4. Run the notebook cells in order.
5. Launch the Gradio interface from the final section.

## Example Prompts

Try prompts like:

- `Explain what diffusion models do in simple terms.`
- `Create a cinematic image of a futuristic city at dusk.`
- `Generate a short video of Batman watching over Gotham City.`

## Project Structure

```text
.
├── Build_a_Multi_Modal_Generation_Agent.ipynb
└── README.md
```

## Notes

- Video generation can require significant GPU memory.
- Generated media quality depends heavily on the model, prompt wording, inference steps, and available hardware.
- The notebook is intended as a learning project and prototype rather than a production-ready application.
