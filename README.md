# NAMMA SPEAK 🗣️
### Your Language, Your Style.

**NAMMA SPEAK** is a Kannada–English code-mixed language assistant designed to convert text between English, Kannada-English code-mixed language, full Kannada script, and casual Romanized Kannada.

The project explores adapting Google's Gemma language model using supervised fine-tuning, LoRA, and the AI4Bharat IndicCMix dataset.

> **Project status:** Prototype under evaluation. The application and training pipeline have been developed, but output quality and the effectiveness of fine-tuning still require verification and improvement.

---

## 📌 Problem Statement

People frequently mix Kannada and English while communicating online. They may use English words, Kannada expressions, informal phrases, Kannada script, and Kannada written using Latin characters in the same conversation.

General-purpose language models may struggle with these variations, particularly informal expressions, transliteration, script conversion, and natural code-mixed phrasing.

NAMMA SPEAK aims to adapt a language model to these communication patterns through supervised fine-tuning and provide an accessible interface for trying different conversion tasks.

## 💡 Proposed Solution

NAMMA SPEAK uses a Gemma base model and a trained LoRA adapter to generate text according to a selected conversion task.

The application provides a Gradio interface where users can enter text, choose a conversion direction, and view the generated output.

The project also compares the original model with the fine-tuned model to investigate whether fine-tuning improves the quality of Kannada-English code-mixed text.

## ✨ Key Features

- Eight Kannada-English language-conversion tasks.
- Gemma-based text generation.
- Parameter-efficient fine-tuning using LoRA.
- Memory-efficient training using Unsloth.
- IndicCMix dataset integration.
- Interactive Gradio interface.
- Base-model versus fine-tuned-model comparison.
- Character-level evaluation using SacreBLEU chrF.
- Evaluation and error-analysis workflow.

*Feature availability depends on the current implementation and successful testing.*

## 🔄 Supported Conversion Tasks

| No. | Input | Output |
|---|---|---|
| 1 | English | Kannada-English code-mixed text |
| 2 | English | Full Kannada script |
| 3 | English | Casual Romanized Kannada |
| 4 | Kannada-English code-mixed text | English |
| 5 | Full Kannada script | English |
| 6 | Romanized Kannada | English |
| 7 | Romanized Kannada | Kannada-English code-mixed text |
| 8 | Kannada-English code-mixed text | Romanized Kannada |

The application uses task-specific instructions to tell the model which output format is required.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Google Colab | Development and training environment |
| NVIDIA T4 GPU | GPU acceleration when available |
| Google Gemma | Base language model |
| Unsloth | Memory-efficient model fine-tuning |
| LoRA / PEFT | Parameter-efficient adaptation |
| Hugging Face Transformers | Model and tokenizer management |
| Hugging Face Datasets | Dataset loading and preprocessing |
| AI4Bharat IndicCMix | Kannada-English code-mixed language dataset |
| SacreBLEU chrF | Character-level similarity evaluation |
| Gradio | Interactive web interface |
| Pandas and NumPy | Data preparation and analysis |

## 🧠 Model Training Approach

NAMMA SPEAK uses supervised fine-tuning to adapt Gemma to the supported conversion tasks.

The training workflow consists of:

1. Authenticate with Hugging Face.
2. Load the permitted Kannada IndicCMix dataset.
3. Inspect the schema and validate the text fields.
4. Clean and preprocess the data.
5. Split original records into training, validation, and test sets.
6. Format task-specific input and target examples.
7. Load the compatible Gemma model using Unsloth.
8. Configure and train a LoRA adapter.
9. Save the adapter and training configuration.
10. Evaluate the base and fine-tuned models on the same held-out examples.
11. Load the trained adapter in the Gradio application.

The actual base-model identifier, package versions, dataset counts, and training settings should be recorded from the executed notebook.

## 📚 Dataset

**Dataset:** AI4Bharat IndicCMix  
**Hugging Face:** https://huggingface.co/datasets/ai4bharat/IndicCMix  
**Intended Kannada file:** `ka.parquet`

Expected text fields include:

- `english`
- `native_script_codemixed`
- `full_native_script`
- `romanized_casual`

These fields must be verified against the actual dataset schema before training. Dataset access may require accepting the dataset's terms or obtaining authorization through Hugging Face.

### Dataset access setup

1. Create a Hugging Face account.
2. Open the IndicCMix dataset page.
3. Complete the required access or consent steps.
4. Create a suitable access token.
5. Open your Google Colab notebook.
6. Open the Secrets panel and create a secret named `HF_TOKEN`.
7. Enable notebook access to the secret.
8. Run the dataset authentication and schema-validation cells.

Never publish your access token or embed it in this repository.

**Data integrity:** The project should use verified dataset records. Any synthetic examples used for testing must be identified as synthetic and must not be presented as genuine IndicCMix data.

## ⚙️ Installation and Setup

### Prerequisites

- A Google account.
- Google Colab.
- Access to the required Hugging Face model and dataset.
- An available GPU runtime, preferably an NVIDIA T4 for the intended configuration.
- The existing project notebook.

### Run the project

1. Open the project's Colab notebook.
2. Select a suitable GPU runtime.
3. Configure the `HF_TOKEN` secret.
4. Install or verify the compatible dependencies specified in the notebook.
5. Run the dataset-access and schema-validation cells.
6. Execute preprocessing and data-splitting cells.
7. Load the existing Gemma model and configure LoRA.
8. Run supervised fine-tuning.
9. Save the trained adapter and configuration.
10. Run the evaluation cells.
11. Launch the Gradio application.

Use the existing notebook's tested package versions rather than blindly upgrading Transformers, TRL, or Unsloth.

### Training configuration

Record the actual values used in your run:

| Parameter | Value |
|---|---|
| Base model identifier | To be recorded from notebook |
| Dataset version or revision | To be recorded |
| Random seed | To be recorded |
| LoRA rank and alpha | To be recorded |
| Learning rate | To be recorded |
| Training epochs | To be recorded |
| Maximum sequence length | To be recorded |
| Training-example count | To be recorded |
| Validation-example count | To be recorded |
| Test-example count | To be recorded |
| GPU | Record actual runtime GPU |

Do not treat suggested configuration values as measured training settings.

## 🌐 Gradio Application

The NAMMA SPEAK interface is designed to provide:

- A text input area.
- A dropdown for selecting a conversion task.
- A Convert button.
- A generated-output area.
- Optional base-versus-fine-tuned comparison.
- Example inputs for demonstrations.

The application should load the correct Gemma base model and trained LoRA adapter. It must not claim to use the fine-tuned model if the adapter has not been loaded successfully.

A temporary Gradio sharing URL can be used for a demonstration when supported by the notebook environment. Such links may expire when the runtime stops.

**Live demo:** Add your verified Gradio URL here.

## 📊 Evaluation

NAMMA SPEAK uses SacreBLEU chrF to compare generated outputs against reference text.

The evaluation should use the same held-out examples for the base and fine-tuned models.

Recommended evaluation measures include:

- Overall chrF score.
- chrF by conversion direction.
- Number of evaluated examples.
- Human-rated naturalness.
- Human-rated meaning preservation.
- Output-format compliance.
- Inference latency.
- Error categories and representative examples.

chrF measures character-level similarity. It does not independently prove semantic correctness, naturalness, or real-world usefulness.

### Current reported experiment

The following values were reported by the current notebook and have not been independently verified.

| Model | Reported chrF |
|---|---:|
| Plain Gemma 4 baseline | 15.15 |
| Fine-tuned Gemma 4 — NAMMA SPEAK adapter | 15.15 |
| Reported difference | 0.00 points |

These preliminary results do **not demonstrate measurable improvement from fine-tuning**.

Further debugging is needed to verify adapter loading, training targets, prompt formatting, generated predictions, and evaluation correctness. Actual test-set size and per-task results should be added after verification.

## 🐛 Current Limitations

- Generated answers may be incorrect or unnatural.
- The current reported chrF score does not show an improvement over the baseline.
- Performance may differ across conversion directions.
- Character-level similarity does not guarantee correct meaning.
- Dialect and informal-expression coverage has not been fully established.
- Human evaluation and broader generalization testing remain necessary.
- Dataset access and field alignment must be verified in the executed environment.

The project should not claim universal Kannada dialect support or superior performance without supporting evidence.

## 🚀 Future Improvements

- Debug incorrect predictions and adapter loading.
- Improve training-target quality and task formatting.
- Increase evaluation coverage using a leakage-free held-out set.
- Report per-task metrics and human ratings.
- Improve handling of informal expressions and transliteration.
- Add automated output-format checks.
- Optimize inference latency and GPU memory use.
- Conduct controlled experiments with different training settings.
- Publish reproducible configuration and evaluation artifacts.

## 📁 Recommended Repository Structure

```text
namma-speak/
├── README.md
├── notebooks/
│   └── namma_speak_finetuning.ipynb
├── src/
│   ├── data_preprocessing.py
│   ├── train.py
│   ├── evaluate.py
│   └── app.py
├── configs/
│   └── training_config.json
├── evaluation/
│   ├── baseline_predictions.csv
│   ├── finetuned_predictions.csv
│   ├── task_metrics
