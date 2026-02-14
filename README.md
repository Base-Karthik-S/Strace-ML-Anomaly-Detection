# Linux Process Anomaly Detection via System Call Analysis

A lightweight, ML-powered host-based intrusion detection prototype that identifies malicious process behavior through statistical analysis of system call patterns.

## 🔍 Overview

This project demonstrates a practical approach to detecting compromised or malicious processes on Linux systems by analyzing deviations from established behavioral baselines. Unlike signature-based detection, this method identifies novel threats based on how they *behave* rather than what they *are*.

## 🏗 Architecture

1. **Tracing Layer**: `strace` captures system call sequences from executables
2. **Feature Extraction**: 10 statistical features derived from raw syscall data
3. **ML Detection**: Unsupervised learning (One-Class SVM / LOF) identifies anomalies
4. **Analyst Interface**: Human-readable reports with confidence scores

## ✨ Features

- **Behavioral Profiling**: Establishes normal process baselines from benign system utilities
- **Anomaly Scoring**: Decision function outputs confidence metrics for each detection
- **Comprehensive Metrics**: Tracks file operations, process creation, network activity, memory manipulation, and security-related syscalls
- **Low False-Positive Design**: Engineered features minimize alert fatigue
- **Model Persistence**: Trained models can be saved and deployed for continuous monitoring

## 🛠 Technical Stack

- **Language**: Python 3.x
- **ML Framework**: Scikit-learn (LocalOutlierFactor, StandardScaler)
- **System Interaction**: Subprocess, Strace
- **Data Processing**: Pandas, NumPy, Collections.Counter
- **Persistence**: Pickle for model serialization

## 📊 Feature Engineering

10 key features extracted from syscall sequences:

| Feature | Description |
|---------|-------------|
| Total Call Count | Overall volume of system calls |
| Unique Call Ratio | Diversity of syscall types |
| File Operation Ratio | Frequency of file I/O operations |
| Process Operation Ratio | Fork/clone/execve frequency |
| Network Operation Ratio | Socket/connect activity |
| Memory Operation Ratio | Mmap/brk/mprotect patterns |
| Security Operation Ratio | Chmod/setuid/capset events |
| Most Frequent Ratio | Dominance of single call type |
| Entropy | Shannon entropy of call distribution |
| Transition Rate | Frequency of call type changes |

## 🚀 Quick Start

```bash
# Clone repository
git clone https://github.com/yourusername/Linux-Process-Anomaly-Detection

# Install dependencies
pip install scikit-learn pandas numpy

# Trace benign binaries and train model
python detector.py --train /path/to/benign/binaries

# Detect anomalies in suspicious files
python detector.py --detect /path/to/suspicious/files
