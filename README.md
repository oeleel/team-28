DJ Song Mixing Recommendation System
Team: Ashley Wu, Bonny Koo, Nathan Suh, Leo Lee
Course: CS 4774 Machine Learning - UVA Fall 2025
Overview
A machine learning system that recommends songs for seamless DJ transitions by combining music theory (BPM, harmonic key compatibility) with audio features. The system compares three approaches: rule-based DJ constraints, audio similarity, and a hybrid ML model.
Problem Statement
DJs spend hours finding compatible songs for mixing. This system automates the process by recommending songs that match based on:

BPM compatibility (±6 BPM ideal for beatmatching)
Key compatibility (Camelot Wheel harmonic mixing)
Energy flow for smooth transitions

Project Structure
team-28/
├── data/
│   └── dataset.csv              # Spotify dataset (download separately)
├── src/
│   ├── main.py                  # CLI interface for recommendations
│   ├── data_preprocessing.py    # Load data, convert to Camelot notation
│   ├── model_rule_based.py      # Model 1: BPM ±6, Camelot key filtering
│   ├── model_audio_similarity.py # Model 2: Cosine similarity baseline
│   ├── model_hybrid_ml.py       # Model 3: XGBoost hybrid system
│   ├── evaluation.py            # Metrics: BPM/key compatibility, energy flow
│   └── utils.py                 # Camelot wheel, search helpers
├── doc/
│   ├── dj_mixing_analysis.ipynb # Main Jupyter notebook with analysis
│   └── project_slides.pptx      # Final presentation
├── requirements.txt
├── QUICKSTART.md
└── README.md
Three Models
Model 1: Rule-Based System
Traditional DJ approach using hard constraints.

Filters songs within ±6 BPM
Requires Camelot Wheel key compatibility
Ranks by weighted score (40% BPM, 35% Key, 20% Energy, 5% Genre)

Model 2: Audio Similarity Baseline
Content-based filtering using cosine similarity.

Compares energy, valence, danceability, acousticness
Ignores BPM/key constraints
Finds similar-sounding songs (but often unmixable)

Model 3: Hybrid ML System
XGBoost classifier combining rules with learned patterns.

Trained on 10,000 song pairs labeled by DJ rules
Features: BPM distance, key compatibility, energy difference
Achieves 100% train/test accuracy

Installation
bash# Clone the repository
git clone https://github.com/oeleel/uva-machine-learning-25f-projects.git
cd uva-machine-learning-25f-projects

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

# Search by Spotify track ID
python main.py --track_id 5SuOikwiRyPMVoIQDJUgSV
Options
--track_id <id>      Spotify track ID (exact match)
--song <name>        Track name (fuzzy matching)
--artist <name>      Artist name (fuzzy matching)
--index <number>     Dataset row index
--data <path>        Path to dataset CSV (default: data/dataset.csv)
--model_path <path>  Path to hybrid ML model (default: hybrid_model.pkl)
--train_model        Force retrain the hybrid ML model
--no_eval            Skip evaluation metrics
Example Output
================================================================================
DJ Mixing Recommendation System
================================================================================

Current Song: Strobe by deadmau5 | BPM: 128.0 | Key: 8A | Energy: 0.85

Rule-Based Recommendations (Top 10)
================================================================================
1. Some Song
   Artist: Some Artist
   BPM: 127.5 | Key: 8A | Energy: 0.82 | Score: 0.9500

Evaluation Metrics
================================================================================
BPM Compatibility: 10/10 (100.0%)
Key Compatibility: 10/10 (100.0%)

Performance Summary
================================================================================
Total Recommendation Time: 0.234 seconds
Target Met: ✓
Dataset

Source: Kaggle Spotify Dataset
Size: 102,596 songs (after cleaning)
Features: tempo, key, mode, energy, valence, danceability, acousticness, instrumentalness, loudness

BPM Statistics

Mean: 123.7
Median: 123.2
Std Dev: 25.1

Top Keys (Camelot Notation)

10B: 8,130 songs
9B: 9,095 songs
8B: 9,108 songs

Camelot Wheel
The Camelot Wheel is the industry standard for harmonic mixing. Compatible keys are:

Same key (e.g., 8A → 8A)
±1 on the wheel (e.g., 8A → 7A or 9A)
Same number, different mode (e.g., 8A → 8B)

Evaluation Metrics

BPM Compatibility Rate: % of recommendations within ±6 BPM
Key Compatibility Rate: % of recommendations with compatible Camelot keys
Energy Flow Score: Smoothness of energy transitions (< 0.3 difference)
Response Time: Target < 1.0 second ✓

Performance
StageTimeFirst run (includes training)2-5 minutesSubsequent runs (cached model)< 1 secondRecommendation generation< 0.3 seconds
References

Camelot Wheel - Harmonic mixing system
Spotify Audio Features - Feature definitions
XGBoost Documentation - ML model

License
This project is for educational purposes as part of UVA CS 4774.
