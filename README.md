# Sinhala Printed OCR - Custom Tesseract Model

This repository contains a custom-trained Tesseract OCR model for recognizing **printed Sinhala text**.

The main trained model file is:

```text
sin_custom_v3.traineddata
```

This model was trained and evaluated as part of a Sinhala OCR research component for extracting Sinhala text from educational documents.

---

## Repository Contents

```text
.
├── sin_custom_v3.traineddata     # Custom trained Tesseract Sinhala OCR model
├── run-wer-cer.ipynb             # Notebook used to evaluate WER and CER
└── README.md                     # Project documentation
```

---

## Model Description

`sin_custom_v3.traineddata` is a custom Tesseract LSTM OCR model trained for **printed Sinhala text recognition**.

The model was trained by the researcher using a Sinhala OCR training dataset containing both printed and handwritten Sinhala samples. For this Tesseract model, the evaluation was focused only on the **printed Sinhala samples**.

---

## Dataset

The dataset used for training and evaluation was:

**Sinhala OCR Training Data**  
Kaggle Dataset:  
https://www.kaggle.com/datasets/hasindukoshitha/sinhala-ocr-training-data

Dataset summary:

| Dataset Detail | Value |
|---|---:|
| Printed samples | 2,840 |
| Successfully processed printed samples | 2,829 |

---

## Training Summary

The custom Tesseract model was trained using the Tesseract LSTM training pipeline. During training, the model showed a significant reduction in internal training error rates.

| Metric | Value |
|---|---:|
| Model name | `sin_custom_v3` |
| OCR engine | Tesseract LSTM |
| Output classes | 117 |
| Total model weights | 940,693 |
| Initial BCER | 22.239% |
| Initial BWER | 50.684% |
| Best BCER | 4.167% |
| BWER at best checkpoint | 14.322% |

The best model checkpoint was selected based on the minimum training **Best Character Error Rate (BCER)**.

---

## Evaluation Results

The model was evaluated using the notebook:

```text
run-wer-cer.ipynb
```

The notebook loads the trained Tesseract model, runs OCR on printed Sinhala image samples, and compares the OCR output with the ground-truth text from `metadata.csv`.

Evaluation was performed using:

- **WER** - Word Error Rate
- **CER** - Character Error Rate

Final printed OCR evaluation results:

| Metric | Value |
|---|---:|
| Average WER | 0.1574 |
| Average WER percentage | 15.74% |
| Average CER | 0.0346 |
| Average CER percentage | 3.46% |

---

## Result Interpretation

The trained Tesseract model achieved a **Character Error Rate of 3.46%** and a **Word Error Rate of 15.74%** on printed Sinhala text samples.

The low CER indicates that the model performs well at recognizing individual Sinhala characters. However, the WER is higher because a word is counted as incorrect even when only one character inside the word is wrongly recognized.

This is especially important in Sinhala OCR because small character, vowel sign, or diacritic errors can change the full word.

---

## How to Use the Model

### 1. Copy the traineddata file

Copy `sin_custom_v3.traineddata` into your Tesseract `tessdata` directory.

Example on Windows:

```text
C:\Program Files\Tesseract-OCR\tessdata
```

Example on Linux:

```bash
/usr/share/tesseract-ocr/4.00/tessdata/
```

or:

```bash
/usr/share/tesseract-ocr/5/tessdata/
```

---

### 2. Run Tesseract from command line

```bash
tesseract input_image.png output -l sin_custom_v3 --oem 3 --psm 6
```

This will generate:

```text
output.txt
```

---

### 3. Use with Python

```python
import pytesseract
from PIL import Image

image = Image.open("sample_image.png")

text = pytesseract.image_to_string(
    image,
    lang="sin_custom_v3",
    config="--oem 3 --psm 6"
)

print(text)
```

---

## Evaluation Notebook

The `run-wer-cer.ipynb` notebook performs the following steps:

1. Loads the dataset metadata.
2. Filters printed Sinhala samples.
3. Runs OCR using `sin_custom_v3`.
4. Compares predicted text with ground-truth text.
5. Calculates WER and CER using the `jiwer` library.
6. Reports average WER and CER.

---

## Requirements for Evaluation

Install the required Python libraries:

```bash
pip install pytesseract pillow pandas jiwer matplotlib
```

Tesseract OCR must also be installed on the system.

---

## Limitations

This model is mainly designed for **printed Sinhala OCR**.

Current limitations include:

- Not optimized for handwritten Sinhala text.
- May struggle with noisy, blurred, skewed, or low-resolution images.
- May produce errors for unsupported symbols, mixed English-Sinhala text, and punctuation.
- Word-level accuracy is lower than character-level accuracy.
- Further improvement is needed for full-page OCR with complex layouts.

---

## Future Improvements

Future improvements may include:

- Expanding the Sinhala character set.
- Cleaning unsupported symbols from training text.
- Adding more printed Sinhala font variations.
- Improving preprocessing for noisy document images.
- Evaluating with a separate unseen test dataset.
- Combining Tesseract printed OCR with a separate handwritten OCR model.

---

## Research Use

This model was developed for Sinhala OCR research and educational document processing. It can be used in Sinhala document digitization pipelines, educational assistant systems, and OCR-based search or question-answering systems.

---

## Model Version

```text
Model name: sin_custom_v3
File: sin_custom_v3.traineddata
OCR engine: Tesseract LSTM
Task: Printed Sinhala OCR
Evaluation CER: 3.46%
Evaluation WER: 15.74%
```

---

## Citation

If this model or dataset is used in academic work, please cite the dataset and mention that the custom Tesseract OCR model was trained for printed Sinhala text recognition.

Dataset:

```text
H. Koshitha, "Sinhala OCR Training Data," Kaggle Dataset.
Available: https://www.kaggle.com/datasets/hasindukoshitha/sinhala-ocr-training-data
```
