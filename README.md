## 🚀 CUGB-M²Rock: A large-scale dataset and benchmark for Martian rock segmentation from images captured by Mars landers and rovers
CUGB-M²Rock is the first large-scale, multi-source benchmark for Martian rock segmentation with 600k+ annotated instances. UBNet achieves leading accuracy with extremely low complexity.

## 🧰 Data Preparation

### 🪨 A. CUGB-M²Rock  
1. Download the dataset from `https://pan.baidu.com/s/1pDYHpmzHCJoakvBEfWX6xw?pwd=wi7v` (access code: `wi7v`).

### 🛰️ B. SynMars  
1. Download the dataset from `https://github.com/CVIR-Lab/SynMars`.

### 🧩 C. Custom Dataset Layout  
1. Organize your custom data as 24-bit PNG images and 8-bit PNG masks (foreground pixels = 255, background = 0):
   ```
   ./your_dataset/
     ├─ images/
     │    ├─ 0000.png
     │    └─ 0001.png
     ├─ masks/
     │    ├─ 0000.png
     │    └─ 0001.png
     └─ Prepare_your_dataset.py
   ```
2. Edit `Prepare_your_dataset.py` to define the training/validation/test splits.
3. Run `Prepare_your_dataset.py` to generate standardized data manifests and indices.

## ⚙️ Environment Setup

Create a dedicated Conda environment (Python 3.8):
```bash
conda create -n ubnet python=3.8
conda activate ubnet
pip install torch==1.13.0 torchvision==0.14.0 torchaudio==0.13.0
pip install causal_conv1d==1.0.0 mamba_ssm==1.0.1
```

## 🧠 Training UBNet

1. Modify `train.py` to set dataset paths, batch size, and logging directories.
2. Default hyperparameters: AdamW, batch size 32 (single GPU), cosine-annealing schedule (initial LR 1e-3, minimum 1e-5), 200 epochs.
3. Start training:
   ```bash
   python train.py
   ```
4. Monitor logs, visualizations, and checkpoints under `./results/`.

## 📊 Evaluation and Inference

1. In `test.py`, set `resume_model` to the desired checkpoint.
2. Run:
   ```bash
   python test.py
   ```
3. Segmentation outputs and metrics are saved in `./results/`.
