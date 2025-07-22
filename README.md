# Firewall Log Analytics AI

An intelligent firewall log analysis system that leverages machine learning to detect anomalies, threats, and security incidents in real-time network traffic data.

## Overview

This project implements a comprehensive security analytics platform that processes firewall logs to:
- Detect network anomalies using machine learning
- Identify potential security threats and suspicious activities
- Provide real-time monitoring dashboards
- Generate actionable security insights

## Features

### Core Analytics
- **Automated Data Processing**: Intelligent preprocessing of firewall log data
- **Feature Engineering**: Advanced feature extraction including traffic patterns, bandwidth utilization, and behavioral indicators
- **Anomaly Detection**: Machine learning-based threat detection using Isolation Forest algorithm
- **Real-time Analysis**: Synthetic timestamp generation for real-time monitoring simulation

### Security Intelligence
- **Threat Detection**: Identifies suspicious activities like port scanning, data exfiltration, and flood attacks
- **Behavioral Analysis**: Monitors unidirectional traffic patterns and unusual bandwidth usage
- **Risk Scoring**: Quantitative anomaly scoring for prioritizing security incidents

### Visualization & Reporting
- **Interactive Dashboards**: Multi-timeframe analysis (hourly, 12-hour, 24-hour intervals)
- **Security Metrics**: Traffic volume, error rates, and threat detection summaries
- **Port Analysis**: Top denied/dropped ports and anomalous destination analysis

## Requirements

### System Requirements
- Python 3.7+
- Jupyter Notebook environment

### Dependencies
All required packages are listed in `requirements.txt`:
- kagglehub>=0.2.0
- pandas>=1.5.0
- numpy>=1.21.0
- matplotlib>=3.5.0
- seaborn>=0.11.0
- scikit-learn>=1.0.0
- joblib>=1.1.0
- jupyter>=1.0.0
- notebook>=6.4.0

## Quick Start

### 1. Clone Repository
```bash
git clone https://github.com/RishabhSpark/firewall-log-analytics-ai.git
cd firewall-log-analytics-ai
```

### 2. Setup Virtual Environment
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
# Install all required packages
pip install -r requirements.txt
```

### 4. Setup Kaggle API (Required for dataset download)
```bash
# Option 1: Install kaggle package and setup API credentials
pip install kaggle
# Then place your kaggle.json in ~/.kaggle/ directory

# Option 2: The notebook will prompt for Kaggle authentication if needed
```

### 5. Launch Jupyter Notebook
```bash
# Start Jupyter Notebook
jupyter notebook

# Open analytics.ipynb in your browser
# Navigate to: http://localhost:8888
```

### 6. Run the Analysis
1. Open `analytics.ipynb` in Jupyter
2. Run all cells sequentially (Cell → Run All)
3. The notebook will:
   - Download the firewall dataset automatically
   - Perform data analysis and feature engineering
   - Train the anomaly detection model
   - Generate security dashboards

## Data Analysis Pipeline

### 1. Data Loading & Exploration
- **Dataset**: Internet Firewall Data (log2.csv)
- **Features**: Source/Destination ports, bytes transferred, packets, elapsed time, actions
- **Size**: Variable based on dataset

### 2. Feature Engineering
The system creates advanced features for better anomaly detection:

- **Traffic Metrics**:
  - `Avg_Packet_Size`: Average bytes per packet
  - `Bytes_Per_Sec`: Bandwidth utilization rate
  - `Packets_Per_Sec`: Packet transmission rate

- **Behavioral Indicators**:
  - `Bytes_Sent_Ratio`: Ratio of sent to received bytes
  - `Packets_Sent_Ratio`: Ratio of sent to received packets
  - `Unidir_Outbound_Flag`: Identifies unidirectional outbound traffic (potential scanning)

### 3. Anomaly Detection Model
- **Algorithm**: Isolation Forest
- **Contamination Rate**: 1% (configurable)
- **Features**: 14 engineered features including traffic patterns and behavioral indicators
- **Output**: Anomaly scores and binary classifications

### 4. Dashboard Generation
Multi-level monitoring dashboard with:
- Traffic volume trends
- Security incident counts
- Top threat vectors
- Port-based analysis

## Model Performance

### Anomaly Detection
- **Model**: Isolation Forest with 100 estimators
- **Preprocessing**: StandardScaler normalization + One-hot encoding
- **Detection Rate**: Configurable contamination parameter (default: 1%)
- **Scoring**: Continuous anomaly scores for threat prioritization

### Key Metrics
- **Anomaly Score**: Lower scores indicate higher anomaly likelihood
- **Binary Classification**: -1 (anomaly) vs +1 (normal)
- **Feature Importance**: Based on isolation path lengths

## Dashboard Insights

### Real-time Monitoring
- **Traffic Analysis**: Bytes transferred over time
- **Error Tracking**: Denied/dropped connection attempts
- **Threat Detection**: Anomaly counts by time period

### Security Intelligence
- **Port Analysis**: Most frequently targeted ports
- **Behavioral Patterns**: Unidirectional traffic detection
- **Threat Prioritization**: Anomaly score-based ranking

## 🔧 Configuration

### Model Parameters
```python
# Isolation Forest Configuration
contamination_rate = 0.01  # Expected anomaly percentage
n_estimators = 100         # Number of isolation trees
random_state = 42          # Reproducibility seed
```

### Feature Selection
The system automatically identifies and processes:
- Numerical features (continuous metrics)
- Categorical features (actions, protocols)
- Engineered features (derived metrics)

## Project Structure

```
firewall-log-analytics-ai/
├── analytics.ipynb              # Main analysis notebook
├── requirements.txt             # Python dependencies
├── data_preprocessor.pkl        # Saved preprocessing pipeline
├── isolation_forest_model.pkl   # Trained anomaly detection model
├── README.md                   # Project documentation
├── LICENSE                     # Project license
├── .gitignore                  # Git ignore rules
└── venv/                      # Virtual environment (created after setup)
```

## Security Use Cases

### 1. Network Intrusion Detection
- Identifies unusual traffic patterns
- Detects port scanning attempts
- Monitors for data exfiltration patterns

### 2. Behavioral Analysis
- Tracks unidirectional communication patterns
- Identifies bandwidth abuse
- Monitors connection duration anomalies

### 3. Threat Hunting
- Provides quantitative threat scoring
- Enables proactive security monitoring
- Supports incident response workflows