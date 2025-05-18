
# Final project for CISC489 exploring protein function prediction using the ProteinChat LLM. Includes prompt engineering experiments and performance analysis.

## 1. Overview
This project evaluates the ProteinChat model for protein function prediction, focusing on experiments with different prompting strategies and text generation parameters. It utilizes the `inference_all.py` script to assess performance based on metrics like Perplexity (PPL), BLEU, and SimCSE scores. This work is based on the ProteinChat framework ("Multi-Modal Large Language Model Enables Protein Function Prediction" by Huo et al.).

## 2. Accessing Project Files (Code, Models, Data)
All essential code (including the Colab notebook `[CISC489 Final Project.ipynb]`, Python scripts like `inference_all.py`, `proteinchat.py`), model checkpoints (Vicuna, Protein Encoder), and data files are bundled here:

**Google Drive Link:** [https://drive.google.com/file/d/1lh4rDeFQc0PQNQ3Q1llcHcWixG8vGJsR/view?usp=sharing](https://drive.google.com/file/d/1lh4rDeFQc0PQNQ3Q1llcHcWixG8vGJsR/view?usp=sharing)

**Instructions:**
1. Download the bundled files from the Google Drive link.
2. Upload the contents to your Google Colab environment (e.g., into a root project folder like `/content/MyProteinChatProject/`) or to your Google Drive and mount it in Colab.
3. Ensure the paths in the Colab notebook and any configuration files (`configs/proteinchat_eval.yaml`) correctly point to these uploaded files, it should work fine if copied from the mounted drive to Colab with the provided code in the notebook.

## 3. Setup in Google Colab

### Dependencies
Run the following commands in a Colab cell to install the necessary libraries:

python
### Ensure PyTorch matches your Colab CUDA version (e.g., cu118 or cu121)
!pip install -U torch torchvision torchaudio --index-url [https://download.pytorch.org/whl/cu118](https://download.pytorch.org/whl/cu118)

### Core libraries
!pip install -U transformers peft accelerate sentencepiece
!pip install -U pandas matplotlib nltk

### Specific libraries for ProteinChat components
!pip install -U iopath decord webdataset deepspeed bitsandbytes omegaconf cpm_kernels

Critical Model Configuration (device_map)
For the LLaMA model (Vicuna) to load correctly on the GPU in 8-bit mode, the device_map parameter must be set.
File: ProteinChat/proteinchat/models/proteinchat.py (within the structure downloaded from Google Drive).
inside the if self.low_resource: block (around line 87 of the discussed proteinchat.py version):
device_map={'': 'cuda:0'}

## 4. Running the Experiments
Open and Prepare Notebook: Open [CISC489 Final Project.ipynb] in Google Colab. Execute initial cells for setup, dependency installation, and data/model path verification.
Modify Parameters (Optional):
Prompts: Edit the questions list in inference_all.py (or the corresponding notebook cell) to test different prompts.
Generation Settings: Adjust temperature, top_p, num_beams in generation_config.json inside vicuna_13b.

Execute Evaluation: Run %%bash
cd /content/ProteinChat
bash demo.sh

## 5. Interpreting Output
Console: View qualitative predictions (Correct vs. Predicted functions), individual losses per protein, and summary metrics:
\\Overall Perplexity (PPL) - Lower is better
\\Execution Time - Lower is better
\\Average BLEU-1 Score - Higher is better
\\Average SimCSE Score - Higher is better
\\Results should be printed since there is an exception of exporting JSON not corrected.


## 6. Acknowledgments
This project is based on the ProteinChat model and utilizes code from the original ProteinChat repository: https://github.com/mignonjia/ProteinChat
Reference Paper: "Multi-Modal Large Language Model Enables Protein Function Prediction" by Huo et al.
