# 🛡️ Dual Watermarking System — Performance & Presentation

> **Role: Person D — Performance Measurement & Final Presentation**
> This module covers accuracy benchmarking, inference timing, and the project presentation slides for the Dual Image Watermarking system using White-Box (LSB) and Black-Box (Trigger Pattern) methods.

---

## 📁 Repository Structure

```
dual-watermark/
├── data/
│   ├── test/
│   │   ├── normal/          # 1000 normal test images
│   │   └── trigger/         # 1000 trigger-embedded test images
│   └── README.md
├── models/
│   ├── whitebox_model.pth   # LSB-based watermarked model
│   └── blackbox_model.pth   # Trigger pattern model
├── scripts/
│   ├── measure_accuracy.py  # Task 1: Accuracy on test set
│   └── measure_inference.py # Task 2: Inference time comparison
├── presentation/
│   └── slides.pptx          # Final presentation deck
├── results/
│   ├── accuracy_results.json
│   └── inference_results.json
├── requirements.txt
└── README.md                # ← You are here
```

---

## ⚙️ Setup & Installation

### Prerequisites

- Python 3.8+
- pip

### Install Dependencies

```bash
pip install -r requirements.txt
```

**`requirements.txt`:**

```
torch>=2.0.0
torchvision>=0.15.0
numpy>=1.24.0
Pillow>=9.5.0
matplotlib>=3.7.0
tqdm>=4.65.0
scikit-learn>=1.2.0
pandas>=2.0.0
```

---

## 📋 Tasks

### ✅ Task 1 — Measure Accuracy on Test Set

**Script:** `scripts/measure_accuracy.py`

Evaluates model accuracy on the test dataset for any given model checkpoint.

#### Usage

```bash
python scripts/measure_accuracy.py \
  --model_path models/whitebox_model.pth \
  --test_dir data/test/normal \
  --model_type whitebox
```

#### Arguments

| Argument | Type | Description |
|---|---|---|
| `--model_path` | `str` | Path to the `.pth` model file |
| `--test_dir` | `str` | Directory containing test images |
| `--model_type` | `str` | `whitebox` or `blackbox` |
| `--batch_size` | `int` | Batch size (default: `32`) |
| `--output` | `str` | Output JSON file path (default: `results/accuracy_results.json`) |

#### Output

```json
{
  "model": "whitebox_model.pth",
  "test_set": "normal",
  "total_images": 1000,
  "correct": 947,
  "accuracy": 94.7,
  "top5_accuracy": 99.1
}
```

---

### ✅ Task 2 — Measure Inference Time

**Script:** `scripts/measure_inference.py`

Compares inference speed between 1000 normal images and 1000 trigger-embedded images.

#### Usage

```bash
python scripts/measure_inference.py \
  --model_path models/blackbox_model.pth \
  --normal_dir data/test/normal \
  --trigger_dir data/test/trigger \
  --model_type blackbox
```

#### Arguments

| Argument | Type | Description |
|---|---|---|
| `--model_path` | `str` | Path to the `.pth` model file |
| `--normal_dir` | `str` | Directory with 1000 normal images |
| `--trigger_dir` | `str` | Directory with 1000 trigger images |
| `--model_type` | `str` | `whitebox` or `blackbox` |
| `--runs` | `int` | Number of timing runs (default: `3`) |
| `--output` | `str` | Output JSON file path (default: `results/inference_results.json`) |

#### Output

```json
{
  "model": "blackbox_model.pth",
  "normal_images": {
    "count": 1000,
    "total_time_ms": 4823.4,
    "avg_per_image_ms": 4.82
  },
  "trigger_images": {
    "count": 1000,
    "total_time_ms": 4891.2,
    "avg_per_image_ms": 4.89
  },
  "overhead_ms": 0.07,
  "overhead_percent": 1.41
}
```

---

### ✅ Task 3 — Presentation Structure

**File:** `presentation/slides.pptx`

The final deck covers the following slides:

| # | Slide | Status |
|---|---|---|
| 1 | Title Slide | ✅ Ready |
| 2 | Problem Statement | ✅ Ready |
| 3 | Solution Overview (Dual Watermark) | ✅ Ready |
| 4 | White-Box Method — LSB Embedding | ✅ Ready |
| 5 | Black-Box Method — Trigger Pattern | ✅ Ready |
| 6 | Performance Impact (Accuracy Chart) | 🔲 Placeholder |
| 7 | Performance Impact (Inference Overhead Chart) | 🔲 Placeholder |
| 8 | Robustness Table *(to be filled by Person C)* | 🔲 Placeholder |
| 9 | Demo Flow | ✅ Ready |
| 10 | Conclusion & Q&A | ✅ Ready |

---

### ✅ Task 4 — Run Performance Measurements

> ⚠️ **Prerequisite:** Models must be ready (provided by Person A/B).

Once models are available, run both measurement scripts in sequence:

```bash
# Step 1: Accuracy for white-box model
python scripts/measure_accuracy.py \
  --model_path models/whitebox_model.pth \
  --test_dir data/test/normal \
  --model_type whitebox

# Step 2: Accuracy for black-box model
python scripts/measure_accuracy.py \
  --model_path models/blackbox_model.pth \
  --test_dir data/test/normal \
  --model_type blackbox

# Step 3: Inference time comparison
python scripts/measure_inference.py \
  --model_path models/blackbox_model.pth \
  --normal_dir data/test/normal \
  --trigger_dir data/test/trigger \
  --model_type blackbox
```

Results will be saved in `results/` and can be used to populate placeholder slides in the presentation.

---

### ✅ Task 5 — Demo & Final Practice

#### Demo Flow

```
1. Show original unprotected model → run inference → no ownership claim possible
2. Embed LSB watermark (white-box) → extract bits → verify ownership
3. Embed trigger pattern (black-box) → query model → backdoor response confirms ownership
4. Show accuracy/inference charts from Task 4
5. Robustness table (filled by Person C)
6. Q&A
```

#### Rehearsal Checklist

- [ ] All scripts run end-to-end without errors
- [ ] Accuracy & inference results exported to `results/`
- [ ] Charts pasted into slides (replace placeholders)
- [ ] Robustness table received from Person C and inserted
- [ ] Full demo rehearsed at least once before presentation day
- [ ] Presentation shared with all team members

---

## 📊 Expected Results (Reference Targets)

| Metric | White-Box (LSB) | Black-Box (Trigger) |
|---|---|---|
| Clean Accuracy | ~94–96% | ~93–95% |
| Watermarked Accuracy | ~93–95% | ~92–95% |
| Accuracy Drop | < 1.5% | < 2% |
| Avg Inference Time (normal) | ~4–5 ms/img | ~4–5 ms/img |
| Avg Inference Time (trigger) | ~4–5 ms/img | ~4–6 ms/img |
| Overhead | < 5% | < 5% |

> These are indicative targets. Actual numbers will be filled after Task 4 completes.

---

## 🤝 Dependencies on Other Team Members

| Person | What D needs from them | When |
|---|---|---|
| Person A | White-box model (`.pth`) | Before Task 4 |
| Person B | Black-box model (`.pth`) | Before Task 4 |
| Person C | Robustness table data | Before Task 3 finalisation |
| Person A/B/C | Availability for demo rehearsal | Task 5 |

---

## 📝 Notes

- Slides can be built immediately with placeholders — **no need to wait for models**.
- Scripts in `scripts/` should be tested with dummy/random weights first to verify they run correctly.
- All results must be saved to `results/` in JSON format for reproducibility.
- Charts for the presentation should be generated using `matplotlib` and exported as `.png` before inserting into slides.

---

## 👤 Author

**Person D** — Performance & Presentation Lead  
Dual Watermarking Project | Team Submission
