# **Fine-Tuned Language Model with LoRA**

Welcome to the repository for our fine-tuned language model using LoRA (Low-Rank Adaptation)! This project demonstrates how we can leverage parameter-efficient fine-tuning to adapt a powerful base language model for generating domain-specific questions. Instead of having the model answer the questions, this setup allows the user to respond with their own answers. 

**Key Links:**
- **Interactive Demo (Gradio)**: [Try the Model Here](https://9b7c23980211fb75b3.gradio.live/)

---

## **Overview**

This project fine-tunes the `unsloth/llama-3.2-3b-instruct-bnb-4bit` base model using LoRA to create a parameter-efficient, specialized language model. The focus of this fine-tuning is to have the model generate coherent, contextually relevant questions about a specific topic. The end-user can then provide their own answers to these questions, facilitating a more interactive and exploratory learning experience.

### **Key Features**
- **Low-Rank Adaptation (LoRA)**: A parameter-efficient fine-tuning technique that modifies specific parts of the model.
- **Topic-Specific Question Generation**: The model is trained to produce well-formed questions that users can answer themselves.
- **Accessible Demo**: A Gradio-based web interface you can access to try out question generation in your browser.

---

## **How to Use**

### **1. Try It Online (Gradio)**

Interact with the model in your browser. The model will generate questions about a certain domain of interest. You, as the user, can then provide your own answers to those questions.

👉 **[Test the Model Here](https://9b7c23980211fb75b3.gradio.live/)**

### **2. Integrate into Your Code**

If you want to integrate the model into your own application to generate questions programmatically:

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

# Load the base tokenizer and LoRA model
tokenizer = AutoTokenizer.from_pretrained("unsloth/llama-3.2-3b-instruct-bnb-4bit", use_fast=False)
model = AutoModelForCausalLM.from_pretrained("Grandediw/lora_model")

# Example prompt
prompt = "Generate a question about historical architecture for the user to answer."
inputs = tokenizer(prompt, return_tensors="pt")
outputs = model.generate(inputs["input_ids"], max_new_tokens=128, temperature=1.5)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

---

## **How It Works**

1. **Base Model**: 
   We start with `unsloth/llama-3.2-3b-instruct-bnb-4bit`, a capable language model optimized for instruction-like tasks.

2. **LoRA Fine-Tuning**: 
   We apply LoRA adapters to select projection layers (`down_proj`, `gate_proj`, `k_proj`, `o_proj`, `q_proj`, `v_proj`, `up_proj`) so that the model can be efficiently specialized to generate questions about a given topic, rather than general text generation or answer completion.

3. **Deployment**:
   The model is served via a Gradio interface, accessible at the provided link. Users can submit prompts asking the model to generate questions, then answer those questions themselves, turning the model into a tool for guided exploration of a subject.

---

## **Model Details**

### **Base Model**
- **Name**: `unsloth/llama-3.2-3b-instruct-bnb-4bit`
- **Task Type**: Causal Language Modeling (CAUSAL_LM)
- **Quantization**: 4-bit for efficient inference.

### **LoRA Configuration**
- **r**: 16
- **lora_alpha**: 16
- **lora_dropout**: 0
- **Target Modules**: `down_proj`, `gate_proj`, `k_proj`, `o_proj`, `up_proj`, `v_proj`, `q_proj`

---

## **Requirements**

### **Dependencies**
```bash
pip install torch transformers peft unsloth gradio
```

### **Environment**
- **Hardware**: NVIDIA GPU recommended for faster inference.
- **Software**: Python 3.8+ and PyTorch 1.12+.

---

## **Try It Yourself**
- Prompt the model to generate a question about a topic of your choice.
- Provide your own answer to explore the subject deeply and interactively.

👉 **[Test the Model](https://9b7c23980211fb75b3.gradio.live/)**

---

## **Acknowledgments**
- **Hugging Face**: For providing the platform and libraries.
- **Unsloth Team**: For their efficient models and tools.
- **LoRA Researchers**: For developing parameter-efficient fine-tuning techniques.

---

**Happy experimenting with the question-generation model!**
