---
layout: default
title: BirdNET Analysis Documentation
---

# BirdNET Analysis Documentation

## Overview
This document outlines the process of using BirdNET-Analyzer to analyze bird vocalizations from AudioMoth recordings. BirdNET is an artificial intelligence system that can identify bird species by sound.

## Setup Process

### 1. Installation
1. Clone the BirdNET-Analyzer repository:
   ```bash
   git clone https://github.com/kahst/BirdNET-Analyzer.git
   cd BirdNET-Analyzer
   ```

2. Install Python 3.11 (required for compatibility)

3. Install required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

4. Download the BirdNET model files:
   - Download the model file from the BirdNET website
   - Place it in the `checkpoints` directory

## Analysis Process

### 1. Running the Analysis
The analysis was run using the following command:
```bash
python analyze.py --i "/path/to/audio/files" --o "/path/to/output" --lat 30.0 --lon -95.0 --week 24 --overlap 0.0 --sensitivity 1.0 --min_conf 0.1
```

Parameters explained:
- `--i`: Input directory containing WAV files
- `--o`: Output directory for results
- `--lat`: Latitude of recording location
- `--lon`: Longitude of recording location
- `--week`: Week of the year (1-48)
- `--overlap`: Overlap between segments (0.0 to 0.9)
- `--sensitivity`: Detection sensitivity (0.5 to 1.5)
- `--min_conf`: Minimum confidence threshold (0.0 to 1.0)

### 2. Combining Results
A custom Python script (`combine_results.py`) was created to:
- Combine all individual CSV result files
- Generate summary statistics
- Create filtered lists based on confidence levels
- Analyze detection patterns

## How BirdNET Works

### Machine Learning Architecture
BirdNET uses a convolutional neural network (CNN) architecture that:
1. Converts audio into spectrograms (visual representation of sound frequencies)
2. Processes these spectrograms through multiple convolutional layers
3. Identifies patterns that correspond to different bird species
4. Outputs confidence scores for each potential species detection

### Key Components
- **Audio Processing**: Converts WAV files into spectrograms
- **Neural Network**: Trained on thousands of bird vocalizations
- **Species Database**: Contains information about 3,000+ bird species
- **Confidence Scoring**: Provides probability scores (0-1) for each detection

## Results Summary

### Overall Statistics
- Total number of detections: 79,224
- Number of unique species detected: 710
- Number of high confidence detections (>0.7): 4,960
- Number of very high confidence detections (≥0.95): 840

### Most Frequently Detected Species
1. Northern Mockingbird (Mimus polyglottos): 5,768 detections
2. Painted Bunting (Passerina ciris): 4,544 detections
3. Northern Cardinal (Cardinalis cardinalis): 4,296 detections
4. Carolina Wren (Thryothorus ludovicianus): 3,992 detections

*Note: The total detection counts above include all detections regardless of confidence level. Some species may have many detections but lower confidence scores, which is why they may not appear in the high confidence lists below. This is common with species that have variable vocalizations or calls that are similar to other species.*

### High Confidence Detections (>0.7)
1. Painted Bunting (Passerina ciris): 1,216 detections
2. Bewick's Wren (Thryomanes bewickii): 448 detections
3. Carolina Wren (Thryothorus ludovicianus): 352 detections
4. Great Horned Owl (Bubo virginianus): 280 detections
5. Eastern Bluebird (Sialia sialis): 176 detections
6. Red-shouldered Hawk (Buteo lineatus): 144 detections
7. Eastern Phoebe (Sayornis phoebe): 128 detections
8. Mississippi Kite (Ictinia mississippiensis): 96 detections
9. Black-crested Titmouse (Baeolophus atricristatus): 32 detections
10. House Finch (Haemorhous mexicanus): 32 detections
11. Barn Swallow (Hirundo rustica): 32 detections
12. Black-bellied Whistling-Duck (Dendrocygna autumnalis): 32 detections
13. Chestnut-winged Cuckoo (Clamator coromandus): 32 detections
14. Common Nighthawk (Chordeiles minor): 32 detections
15. European Greenfinch (Chloris chloris): 32 detections
16. Barn Owl (Tyto alba): 32 detections

*Note: The system also detected some non-bird sounds with high confidence, including vehicle engine noise and a pet dog. These detections have been excluded from the above list as they are not relevant to the bird species analysis.*

### Very High Confidence Detections (≥0.95)
1. Painted Bunting (Passerina ciris): 312 detections
2. Bewick's Wren (Thryomanes bewickii): 192 detections
3. Red-shouldered Hawk (Buteo lineatus): 48 detections
4. Great Horned Owl (Bubo virginianus): 48 detections
5. Eastern Bluebird (Sialia sialis): 40 detections
6. Carolina Wren (Thryothorus ludovicianus): 32 detections
7. Eastern Phoebe (Sayornis phoebe): 32 detections
8. Mississippi Kite (Ictinia mississippiensis): 24 detections
9. Black-crested Titmouse (Baeolophus atricristatus): 8 detections
10. House Finch (Haemorhous mexicanus): 8 detections
11. Barn Swallow (Hirundo rustica): 8 detections
12. Black-bellied Whistling-Duck (Dendrocygna autumnalis): 8 detections
13. Chestnut-winged Cuckoo (Clamator coromandus): 8 detections
14. Common Nighthawk (Chordeiles minor): 8 detections
15. European Greenfinch (Chloris chloris): 8 detections
16. Barn Owl (Tyto alba): 8 detections

*Note: The system also detected some non-bird sounds with very high confidence, including vehicle engine noise and a pet dog. These detections have been excluded from the above list as they are not relevant to the bird species analysis.*

## Understanding the Results

### Confidence Scores
- Scores range from 0 to 1
- Higher scores indicate greater confidence in the detection
- Recommended thresholds:
  - High confidence: >0.7
  - Very high confidence: ≥0.95

### Output Files
- Individual CSV files for each audio file
- Combined results file with all detections
- Summary files for different confidence levels
- Time-based analysis of detections

## Notes and Limitations
- BirdNET detects bird calls/songs, not individual birds
- Multiple detections of the same species could be from:
  - The same bird making multiple calls
  - Multiple birds of the same species
  - Background noise or similar sounds
- Results should be considered as presence/absence data rather than population counts

## References
- BirdNET-Analyzer GitHub: https://github.com/kahst/BirdNET-Analyzer
- BirdNET Project: https://birdnet.cornell.edu/
- AudioMoth: https://www.openacousticdevices.info/ 