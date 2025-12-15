<<<<<<< HEAD
# DJ Mixing Recommendation System

A machine learning system that recommends mixable songs for DJs based on BPM, musical key, and energy flow. The system implements three models: Rule-Based, Audio Similarity Baseline, and Hybrid ML (XGBoost).

## Project Structure

```
team-28/
├── src/                    # All source code
│   ├── main.py            # Main execution script
│   ├── data_preprocessing.py
│   ├── model_rule_based.py
│   ├── model_audio_similarity.py
│   ├── model_hybrid_ml.py
│   ├── evaluation.py
│   ├── utils.py
│   └── visualize_results.py
├── doc/                    # Documentation
│   └── QUICKSTART.md
├── data/                   # Dataset
│   └── dataset.csv
├── requirements.txt        # Python dependencies
├── hybrid_model.pkl        # Trained ML model (generated)
└── README.md              # This file
```

## Features

- **Three Recommendation Models:**
  - Rule-Based: Uses hard constraints (BPM ±6, key compatibility)
  - Audio Similarity: Content-based filtering using cosine similarity
  - Hybrid ML: XGBoost model combining DJ rules with audio features

- **Multiple Search Methods:**
  - Search by track ID, song name, artist, or dataset index
  - Fuzzy matching with exact match preference

- **DJ Mixing Rules:**
  - BPM compatibility (±6 BPM tolerance)
  - Camelot Wheel key compatibility
  - Energy flow analysis
  - Genre matching

## Usage

### Basic Usage

Run from the project root directory:

```bash
# Search by song and artist
python src/main.py --song "Strobe" --artist "deadmau5"

# Search by track ID
python src/main.py --track_id 5SuOikwiRyPMVoIQDJUgSV

# Search by song name only
python src/main.py --song "Strobe"

# Search by artist
python src/main.py --artist "deadmau5"

# Search by index
python src/main.py --index 0
```

### Command-Line Options

```
--track_id <id>        Spotify track ID (exact match)
--song <name>          Track name (fuzzy matching)
--artist <name>        Artist name (fuzzy matching)
--index <number>       Dataset row index
--data <path>          Path to dataset CSV (default: ../data/dataset.csv)
--model_path <path>    Path to hybrid ML model (default: ../hybrid_model.pkl)
--train_model          Force retrain the hybrid ML model
--no_eval              Skip evaluation metrics
```

### Generate Visualizations

```bash
python src/visualize_results.py
```

## Documentation

See `doc/QUICKSTART.md` for detailed usage instructions and troubleshooting.

## Requirements

- Python 3.7+
- pandas >= 1.5.0
- numpy >= 1.23.0
- xgboost >= 1.7.0
- scikit-learn >= 1.1.0
- matplotlib >= 3.5.0
- seaborn >= 0.12.0

# Install dependencies
pip install -r requirements.txt
Requirements
pandas>=1.5.0
numpy>=1.23.0
xgboost>=1.7.0
scikit-learn>=1.1.0
Dataset
Download the Spotify dataset from Kaggle and place it at data/dataset.csv.
Usage
Command Line Interface
bash# Search by song name and artist
python main.py --song "Strobe" --artist "deadmau5"

# Search by song name only (fuzzy matching)
python main.py --song "Blinding Lights"

# Search by dataset index
python main.py --index 0
