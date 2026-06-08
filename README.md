# CUGB-M²Rock

**A Large-Scale Martian Rock Dataset and a Spatial-Frequency Dual-Domain Mamba for Martian Rock Segmentation**

> ⚠️ **Under peer review.** This manuscript has not yet been published. For citation guidance or updates, please contact the corresponding authors.

CUGB-M²Rock is the first large-scale, multi-source benchmark for Martian rock segmentation from images captured by Mars landers and rovers, with **600k+** annotated instances. **UBNet** achieves leading accuracy with extremely low complexity.

---

## Authors & Affiliations

**Shiyang Fu**<sup>1,2</sup> · **Xiaoman Qi**<sup>1,2</sup> · **Yuebin Wang**<sup>1,2</sup>\* · **Zhizhong Kang**<sup>1,2</sup>\* · **Liqiang Zhang**<sup>3</sup> · **Huan Xie**<sup>4,5</sup>

| | Affiliation |
|:---|:---|
| <sup>1</sup> | School of Land Science and Technology, China University of Geosciences (Beijing), Beijing 100083, China |
| <sup>2</sup> | Subcenter of International Cooperation and Research on Lunar and Planetary Exploration, Center of Space Exploration, Ministry of Education of The People's Republic of China, Beijing 100083, China |
| <sup>3</sup> | Key Laboratory of Environmental Remote Sensing and Digital Cities, Faculty of Geographical Science, Beijing Normal University, Beijing 100875, China |
| <sup>4</sup> | Shanghai Research Institute for Intelligent Autonomous Systems and College of Surveying and Geo-informatics, Tongji University, Shanghai 200092, China |
| <sup>5</sup> | Shanghai Key Laboratory for Planetary Mapping and Remote Sensing for Deep Space Exploration, Tongji University, Shanghai 200092, China |

\*Corresponding authors: [Yuebin Wang](mailto:wangyuebin@cugb.edu.cn) · [Zhizhong Kang](mailto:zzkang@cugb.edu.cn)

---

## Data Preparation

### A. CUGB-M²Rock

Download the dataset from [Baidu Pan](https://pan.baidu.com/s/1qHHYl3sZF42LMVnisO9chg?pwd=fsxh) (access code: `fsxh`).

### B. SynMars

Download the dataset from [CVIR-Lab/SynMars](https://github.com/CVIR-Lab/SynMars).

### C. Custom Dataset Layout

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

---

## Environment Setup

Create a dedicated Conda environment (Python 3.8):

```bash
conda create -n ubnet python=3.8
conda activate ubnet
pip install torch==1.13.0 torchvision==0.14.0 torchaudio==0.13.0
pip install causal_conv1d==1.0.0 mamba_ssm==1.0.1
```

---

## Training UBNet

1. Modify `train.py` to set dataset paths, batch size, and logging directories.
2. Default hyperparameters: AdamW, batch size 32 (single GPU), cosine-annealing schedule (initial LR 1e-3, minimum 1e-5), 200 epochs.
3. Start training:

   ```bash
   python train.py
   ```

4. Monitor logs, visualizations, and checkpoints under `./results/`.

---

## Evaluation and Inference

1. In `test.py`, set `resume_model` to the desired checkpoint.
2. Run:

   ```bash
   python test.py
   ```

3. Segmentation outputs and metrics are saved in `./results/`.
