# MIMO-5G-Network-Throughput-Prediction

## Problem Setting
The topology below shows a 5G two-tier cellular MIMO-OFDMA system. The cells are hexagonal and a base station (BS) is located at the center of each cell. We aim to predict and classify user throughput in this network based on a variety of network and user-related parameters. The dataset contains both numerical and categorical features describing each user’s position, connection parameters, and signal characteristics. More specifically, we utilize the following features.

- x, y user coordinates in the topology
- base station (BS) of service
- sector of service
- modulation type (QPSK, 16-QAM, 64-QAM)
- signal strength
- user-BS distance
- user-BS angular distance

## Approach

### Feature Engineering

- Encoded categorical ModulationType using LabelEncoder.

- Applied square root transformation to Power_W_ to reduce skew.

- Represented angles using sine and cosine to handle cyclicity.

- Removed redundant features after correlation analysis.

### Regression Task

- Target: continuous throughput (Throughput_Mbps_).

- Scaled features to [-1, 1] and target to [0, 1] for MLP compatibility.

- Used MLPRegressor with tanh activation, early stopping, and 5-fold cross-validation to tune:

- Hidden layer sizes

- Optimizer type

- Learning rate & schedule

### Classification Task

- Converted throughput into binary classes:

    - Class 0: ≤ 300 Mbps

    - Class 1: > 300 Mbps

- Tested two models: SVC (with polynomial kernel, class weighting, and scaling) and DecisionTreeClassifier.

- Used HalvingGridSearchCV for efficient hyperparameter tuning.

- Evaluated models using macro F1-score and classification reports.
</p>