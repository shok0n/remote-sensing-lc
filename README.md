# Remote Sensing for Land Cover Detection

Course project for **MLESS — Machine Learning for Earth System Science**
(Prof. Dr. Martin Schultz, University of Cologne).

This repository compares two machine learning approaches — a **Random Forest**
classifier and a **Convolutional Neural Network (CNN)** — on a scene-level land
cover classification task using satellite remote sensing imagery.

> **Status:** Repository is set up; baseline notebooks adopted from the course
> material. Experiments, results, and discussion will be added as the project
> progresses.

---

## Task Description

Given a small satellite image, predict which of six land cover classes it
depicts:

1. Barren land
2. Trees
3. Grassland
4. Roads
5. Buildings
6. Water bodies

The classification is performed at the **scene level**: each 28×28-pixel image
is assigned a single label representing the dominant land cover type.

The objectives of the project are to:

- Train and evaluate a Random Forest classifier on flattened pixel features.
- Train and evaluate a CNN classifier on the same data.
- Compare the two approaches in terms of **predictive quality**, **training
  time**, and **inference time**.
- Identify network and training parameters worth tuning to improve results.

---

## Dataset

The data is a subset of the [**SAT-6**](https://csc.lsu.edu/~saikat/deepsat/)
dataset:

> Saikat Basu, Sangram Ganguly, Supratik Mukhopadhyay, Robert Dibiano, Manohar
> Karki, Ramakrishna Nemani. *DeepSat — A Learning Framework for Satellite
> Imagery.* ACM SIGSPATIAL 2015.

- **Image size:** 28 × 28 pixels
- **Channels:** 4 (red, green, blue, near-infrared)
- **Pixel type:** `uint8`
- **Classes:** 6 land cover types (see above)
- **Subset used:** the original SAT-6 *test* split, which is sufficient for
  educational experiments.

The original SAT-6 data is not available for free anonymous download. A subset
mirror is hosted on the FZ Jülich B2SHARE server:

<https://b2share.eudat.eu/records/89654eac10724d30a6c7e51f2c5422de>

### Getting the data

Download the three data files and place them in a `data/` directory at the
repository root:

```
remote-sensing-lc/
├── data/
│   ├── <X file>
│   ├── <y file>
│   └── <annotations / class names>
├── Random_forest_classifier_on_remote_sensing_image.ipynb
└── CNN_classifier_on_remote_sensing_image.ipynb
```

The `data/` directory is gitignored.

---

## Methods

### Random Forest baseline

Notebook: [`Random_forest_classifier_on_remote_sensing_image.ipynb`](Random_forest_classifier_on_remote_sensing_image.ipynb)

- Loads the SAT-6 subset into pandas.
- Treats each image as a flat feature vector (28 × 28 × 4 = 3136 features).
- Trains a `RandomForestClassifier` from scikit-learn.
- Evaluates accuracy and per-class metrics.

> **Note:** loading the data into pandas requires roughly **5 GB of RAM**.
> Make sure your Jupyter environment has enough memory.

### Convolutional Neural Network

Notebook: [`CNN_classifier_on_remote_sensing_image.ipynb`](CNN_classifier_on_remote_sensing_image.ipynb)

- Uses PyTorch.
- Input: 4-channel 28×28 image tensors.
- Architecture, optimiser, loss function, and training schedule are documented
  in the notebook.
- Evaluates accuracy and per-class metrics, comparable to the Random Forest
  baseline.

Requires a working **PyTorch** installation (CPU is sufficient for this
dataset; a GPU will speed training up but is not required).

---

## Setup

### Requirements

- Python 3.10+
- Jupyter Lab / Notebook
- `numpy`, `pandas`, `scikit-learn`, `matplotlib`
- `torch`, `torchvision` (for the CNN notebook)

A minimal install with pip:

```bash
pip install numpy pandas scikit-learn matplotlib jupyterlab torch torchvision
```

### Running the notebooks

1. Place the dataset files in `data/` (see above).
2. Start Jupyter Lab from the repository root:
   ```bash
   jupyter lab
   ```
3. Run **`Random_forest_classifier_on_remote_sensing_image.ipynb`** first to
   establish the baseline.
4. Then run **`CNN_classifier_on_remote_sensing_image.ipynb`** and compare.

---

## Notebook Questions

The notebooks contain questions to be answered as part of the assignment.
Answers are collected here in the README rather than in the notebooks
themselves.

### Random Forest notebook

*To be filled in.*

### CNN notebook

*To be filled in.*

---

## Results

*To be filled in once experiments are run.*

| Model         | Accuracy | Training time | Inference time | Notes |
| ------------- | -------- | ------------- | -------------- | ----- |
| Random Forest | _TBD_    | _TBD_         | _TBD_          |       |
| CNN           | _TBD_    | _TBD_         | _TBD_          |       |

Confusion matrices, per-class precision/recall, and example predictions will
be added here.

---

## Discussion

*To be filled in.* Planned points to address:

- Where does each model do well / poorly, and why?
- Cost/benefit trade-off: is the CNN's added complexity justified by accuracy
  gains on this dataset?
- Which CNN hyperparameters (depth, channel widths, learning rate, batch size,
  augmentation) most affect results?
- How would the picture change with the full SAT-6 training set rather than
  just the test subset?

---

## Repository Layout

```
.
├── README.md
├── FEEDBACK.md                                              # course feedback
├── LICENSE
├── Random_forest_classifier_on_remote_sensing_image.ipynb
├── CNN_classifier_on_remote_sensing_image.ipynb
└── data/                                                    # gitignored
```

---

## Acknowledgements

- Course material adapted from the MLESS lecture by Prof. Dr. Martin Schultz
  (University of Cologne, April 2026).
- SAT-6 dataset by Basu et al. (2015).

## License

See [LICENSE](LICENSE).
