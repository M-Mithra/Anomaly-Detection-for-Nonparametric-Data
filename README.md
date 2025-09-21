# Anomaly-Detection-for-Nonparametric-Data

This document outlines the implementation of a **Sequential Nonparametric (NP-SEQ)** test for detecting anomalous data streams, based on the methodology presented in the paper **"Sequential Nonparametric Detection of Anomalous Data Streams"** by Sreeram C. Sreenivasan and Srikrishna Bhashyam.

The provided Python script simulates various data streams to evaluate the performance of a test that identifies a statistically different stream without relying on assumptions about the underlying data distributions.

-----

## Project Overview

The core objective of this project is to demonstrate the efficiency and robustness of a sequential anomaly detection test. The algorithm functions by:

1.  **Sequentially collecting data** from multiple streams.
2.  **Calculating the Maximum Mean Discrepancy (MMD)** as a measure of statistical distance between each stream and the aggregated data from all other streams.
3.  **Comparing this distance to a decaying threshold** ($T\_n = C / n^\\alpha$).
4.  **Stopping the test** as soon as the threshold is exceeded to declare an anomaly.

This methodology is highly valuable for applications requiring rapid anomaly detection, such as **real-time systems** where minimizing the number of samples and the detection time is critical.

-----

## How It Works

### Core Concepts

  * **Nonparametric Test:** The test is distribution-free, meaning it operates without assuming a specific data distribution (e.g., Gaussian). This universal applicability enhances its utility across diverse datasets.
  * **Maximum Mean Discrepancy (MMD):** The MMD serves as the statistical metric for quantifying the dissimilarity between probability distributions, allowing the test to identify subtle deviations from the norm.
  * **Sequential Testing:** The adaptive nature of the test, which stops as soon as a decision can be made with high confidence, offers a significant efficiency advantage over conventional fixed-sample-size tests.
  * **Decaying Threshold:** The threshold diminishes with an increasing number of samples ($n$). This adaptive sensitivity ensures that the test becomes capable of detecting more subtle anomalies as more data is collected.

### Functions

  * `compute_mmd2_fast(x, y, sigma)`: This function calculates the **Maximum Mean Discrepancy (MMD)** value between two data streams. It is used as the distance metric to determine how statistically different two streams are.
  * `sample_p(n)` and `sample_q(n)`: These functions generate data for the simulations. `sample_p(n)` creates samples from a "typical" (normal) distribution, while `sample_q(n)` creates samples from an "anomalous" distribution, simulating the two types of data streams.
  * `np_seq_test(...)`: This is the main function that runs the simulation. It manages the sequential collection of samples, calculates MMD values, applies the decaying threshold, and records performance metrics such as stopping time and error for each trial.

### Simulation Parameters

The script's behavior can be controlled by modifying key parameters:

  * **`S`**: The total number of data streams.
  * **`num_trials`**: The number of simulation runs to ensure statistical robustness.
  * **`max_steps`**: A safeguard against infinite loops by setting a maximum number of samples.
  * **`alpha`**: The exponent governing the decay rate of the threshold.
  * **`C`**: The confidence parameter that scales the threshold, influencing the balance between test accuracy and speed.

-----

## Usage

### Dependencies

The following Python libraries are required to run the script:

```bash
pip install numpy pandas matplotlib tqdm
```

### Running the Script

1.  Modify the simulation parameters in the `SETTINGS` section of the script.
2.  Execute the script from the terminal.

<!-- end list -->

```bash
python <your_script_name>.py
```

3.  You will be prompted to provide a folder name for saving the output files.

-----

## Outputs

The script generates the following outputs for analysis:

  * **An Excel file (`.xlsx`)**: This file contains a comprehensive record of the simulation results, including the average stopping time ($\\mathbb{E}[N]$), error probability ($P\_{\\max}$), and MMD values for each tested (`alpha`, `C`) combination.
  * **A Plot (`.png`)**: A plot is created that visually represents the trade-off between the test's efficiency and its accuracy, providing a clear comparison of the different parameter settings.

-----

Authored by **M. A. Rama Murthy**.
