# Urdu to Roman Urdu Translation Model

This project aims to build a **sequence-to-sequence (Seq2Seq) model** for **translating Urdu text** into **Roman Urdu** using a **BiLSTM** encoder and **LSTM** decoder architecture. The model uses **Byte Pair Encoding (BPE)** for tokenization and is trained on the **Urdu Ghazals dataset**.

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Dataset](#dataset)
4. [Model Architecture](#model-architecture)
5. [Training](#training)
6. [Evaluation](#evaluation)
7. [Inference](#inference)
8. [Contributing](#contributing)
9. [License](#license)

## Introduction

This repository provides the implementation of a **BiLSTM-based neural machine translation model** for the transliteration of **Urdu text** to **Roman Urdu**. The model uses **Byte Pair Encoding (BPE)** to handle the vocabulary and character-level translations.

## Installation

To get started with the project, you can clone this repository and install the required dependencies.

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/urdu-to-roman-urdu.git
   cd urdu-to-roman-urdu
   ```

2. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

   **Dependencies**:

   * PyTorch
   * sacrebleu
   * editdistance
   * sklearn
   * pandas
   * numpy

## Dataset

The dataset used in this project is the **Urdu Ghazals dataset** from [this repository](https://github.com/amir9ume/urdu_ghazals_rekhta). This dataset includes **Urdu poetry** (Ghazals) along with **Roman Urdu transliterations** and **English transliterations**.

The dataset contains:

* Urdu text (source)
* Roman Urdu transliteration (target)

The dataset is **downloaded and unzipped** automatically when running the code.

```bash
git clone https://github.com/amir9ume/urdu_ghazals_rekhta.git
unzip -q urdu_ghazals_rekhta/dataset/dataset.zip -d urdu_ghazals_rekhta/dataset/
```

## Model Architecture

The model uses a **BiLSTM-based Seq2Seq architecture**:

* **BiLSTM Encoder**: Encodes the source (Urdu) text into a fixed-length vector, capturing both forward and backward context.
* **LSTM Decoder**: Decodes the fixed-length vector into the target Roman Urdu text.
* **Byte Pair Encoding (BPE)**: Applied for tokenization on the Roman Urdu side to handle subword-level segmentation.

The model uses two layers for the **BiLSTM encoder** and four layers for the **LSTM decoder**, as per the assignment specifications.

## Training

1. **Preprocessing**:

   * The Urdu and Roman Urdu pairs are extracted and cleaned.
   * We normalize the Roman Urdu text and clean the Urdu text by removing unwanted characters and spaces.

2. **Vocabulary**:

   * A **character-level vocabulary** is built for both Urdu (source) and Roman Urdu (target).
   * **Padding tokens** (`<pad>`, `<sos>`, `<eos>`, `<unk>`) are included.

3. **Training Procedure**:

   * The data is split into **50% training**, **25% validation**, and **25% testing**.
   * We use **CrossEntropyLoss** and the **Adam optimizer** to train the model.
   * Early stopping is implemented based on validation loss to avoid overfitting.

4. **Metrics**:

   * **BLEU Score**: Measures the quality of translations against references.
   * **Perplexity**: Measures how well the model predicts the next token.
   * **Character Error Rate (CER)**: Measures the number of character-level edits required to match the predicted text with the reference.

## Evaluation

After training the model, we evaluate its performance using **BLEU**, **Perplexity**, and **CER** on the test dataset. The evaluation script loads the best model checkpoint and computes these metrics.

## Inference

The model can also be used to make predictions for new **Urdu** sentences. The `translate_sentence` function performs **beam search** decoding to generate the Roman Urdu transliteration of the input sentence.

Example:

```python
sample_urdu = "تمہارا نام کیا ہے؟"
predicted_roman = translate_sentence(model, sample_urdu)
print(f"Input Urdu: {sample_urdu}")
print(f"Predicted Roman Urdu: {predicted_roman}")
```

## Contributing

Feel free to fork this repository, contribute to the code, or suggest improvements. Please ensure that your contributions adhere to the coding standards of this project.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Note:

Ensure to install the required dependencies and download the dataset before running the model. If you run into any issues, feel free to open an issue in the repository.

---
