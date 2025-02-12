# Fake Social MEdia Detection

Detecting fake profiles using keystroke dynamics.

---

## 🎯 Project Goal

Develop a lightweight system to identify fake profiles on social media platforms using keystroke features.

---

📂 Repository Structure:
```

📦 social-network-fake-profile-detection
│
├── 📁 features/              # Scripts for extracting key features
│   ├── 📝 word_parser.py     # Extracts word-level features
│   ├── 📝 keystroke_features.py  # Extracts keystroke-based authentication features
│
├── 📁 verifiers/             # Verification algorithms to detect fake profiles
│   ├── 📝 template_generator.py  # Processes keystroke data into templates
│   ├── 📝 verifier_library.py    # Contains various verifier algorithms
│   ├── 📝 AbsoluteVerifier.py    # Exact keystroke pattern comparison
│   ├── 📝 SimilarityVerifier.py  # Measures keystroke similarity
│   ├── 📝 ITAD.py                # Implements the Inter-Tap Action Duration method
│
├── 📁 fusion/                # Enhances detection accuracy using multiple verification methods
│   ├── 📝 score_level_fusion.py   # Combines multiple verification scores using statistical methods
│   ├── 📝 decision_level_fusion.py  # Applies thresholds to determine profile authenticity
│
├── 📁 heatmap/               # Visualizations for detecting fake profiles
│   ├── 📝 heatmap_generator.py  # Generates heatmaps from keystroke dynamics
│
├── 📝 config.py              # Configuration settings for feature selection, word holders, and gender-based filtering
├── 📝 requirements.txt       # Dependencies and libraries required for the project
├── 📝 LICENSE                # License information
├── 📝 README.md              # Project documentation and usage instructions

```
---


## 🔍 Overview of the Key Parts of the Code Base

![Workflow](media/Worflow.jpg)

### 1. Features

- Word level features are extracted from the `features/word_parser` file.
- Keystroke features (KHT & KIT) are extracted from the `features/keystroke_features` file.

### 2. Verifiers

- **Template Generator**: Processes our compact CSV file containing keystroke data.
- **Verifier Library**: A set of verifier algorithms implemented as class methods for easy usage. These include:
  - Absolute Verifier
  - Similarity Verifier
  - ITAD

### 3. Fusion

- **Score Level Fusion**: Features several fusion algorithms:
  - Mean
  - Median
  - Min
  - Max

  Fusion scores are derived by iterating over the ITAD, Absolute, and Similarity matrices. These scores are then employed to determine the `top_k_accuracy_score` ranging from k=1 to k=5.

- **Decision Level Fusion**: Fusion at the score level is determined using empirically set thresholds specific to each verifier. Profiles are labeled genuine or otherwise based on the outcome.

### 4. Heatmap Generation

Generates a heatmap using a matrix of the scores from a particular verifier algorithm for all user IDs. The scores are derived from keystroke features and, optionally, word-level features.

For example, this is an example heatmap with probe and enrollment IDs
both for Facebook , combining KHT and KIT Flight 1 features, using all available session IDs, and the similarity verifier as the algorithm:
![HeatmapExample](media/heatmap_example.png)

### 5. Configuration File

Configure experimental conditions via the config file:

- `use_feature_selection`: Opt for feature selection with **true** or skip with **false**.
- `use_word_holder`: Decide to use word level features with **true** or avoid with **false**.
- `gender`: Choose the gender data to incorporate:
  - **all**: All IDs
  - **male**: Male IDs only
  - **other**: Other IDs only

## 🚀 Getting Started

### Prerequisites

Ensure you have Python 3.x installed. Install the required dependencies:

```sh
pip3 install -r requirements.txt
```

Running the Application
Feature Extraction: Use scripts in the features/ directory to extract word-level and keystroke features from your dataset.

Template Generation: Process the extracted features using the template_generator.py script in the verifiers/ directory.

Verification: Apply verifier algorithms from the verifier_library.py to assess profile authenticity.

Fusion: Enhance detection accuracy by combining verifier scores using fusion techniques in the fusion/ directory.

Visualization: Generate heatmaps using heatmap_generator.py to visualize verifier scores across user IDs.

Now you are ready to go and can run any of the runnable scripts
