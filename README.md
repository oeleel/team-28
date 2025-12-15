# DJ Mixing Recommendation System

A machine learning system that recommends mixable songs for DJs based on BPM, musical key, and energy flow. The system implements three models: Rule-Based, Audio Similarity Baseline, and Hybrid ML (XGBoost).

## Project Structure

```
team-x/
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

## Installation

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Ensure dataset is at `data/dataset.csv`

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

This generates plots in the `plots/` directory showing:
- BPM distribution
- Key distribution
- Energy distribution
- Audio features correlation
- Model comparison
- Feature importance

## First Run

On the first run, the system will:
1. Load and preprocess the dataset (~114,000 tracks)
2. **Train the hybrid ML model** (takes 2-5 minutes)
3. Save the model to `hybrid_model.pkl` for future use

Subsequent runs will load the pre-trained model (much faster).

## Model Details

### Rule-Based Model
- Filters by BPM ±6 and key compatibility
- Ranks by BPM distance, key score, and energy flow
- Weights: 40% BPM, 35% Key, 20% Energy, 5% Genre

### Audio Similarity Model
- Uses cosine similarity on audio features
- Adds bonuses for BPM/key/energy compatibility
- Ignores strict DJ rules (baseline comparison)

### Hybrid ML Model
- XGBoost classifier trained on synthetic labels
- Combines DJ mixing rules with audio features
- Post-processing boosts for BPM/key/energy compatibility

## Evaluation Metrics

The system evaluates recommendations on:
- **BPM Compatibility**: % within ±6 BPM (target: 100%)
- **Key Compatibility**: % with compatible keys (target: 80%+)
- **Energy Flow**: Average energy difference (target: smooth transitions)
- **Response Time**: Must be < 1 second

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

## License

See LICENSE file for details.
