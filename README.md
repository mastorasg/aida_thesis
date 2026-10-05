# Reinforcement Learning-Based Stock Trading

A research-oriented project that applies reinforcement learning to automated stock trading using historical market data, technical indicators, model evaluation, and Interactive Brokers integration.

This repository accompanies the master's thesis:

> **Reinforcement Learning-Based Stock Trading: Training Evaluation and Integration of an Agent into a Brokerage Platform Bot**  
> Georgios Mastoras  
> MSc Thesis, Department of Applied Informatics  
> University of Macedonia, 2025

The project explores whether reinforcement-learning agents can learn trading decisions from historical market data. It compares multiple RL algorithms, evaluates their results through backtesting, and uses the final trained agent in an Interactive Brokers trading workflow.

> ⚠️ **Educational and research use only.** This project is not financial advice, investment advice, or a guarantee of future profitability. Trading involves substantial risk, including the possible loss of invested capital.

## Overview

The project builds a reinforcement-learning trading agent that receives market information, selects an action, and receives a reward based on the outcome of that action.

The research workflow includes:

- Retrieving and preparing historical market data.
- Analysing market data and technical indicators.
- Training and comparing RL algorithms.
- Evaluating models with train, test, and evaluation data.
- Selecting and training a final model.
- Connecting the final trained model to Interactive Brokers.

The final implementation uses **Interactive Brokers**. Commented OANDA-related code may remain from earlier experiments, but it is not part of the final active trading workflow.

## Algorithms

The project compares the following reinforcement-learning algorithms from Stable-Baselines3:

| Algorithm | Type | Purpose in this project |
|---|---|---|
| DQN | Value-based reinforcement learning | Baseline model for algorithm comparison |
| A2C | Actor-critic reinforcement learning | Alternative policy-learning approach |
| PPO | Policy-optimization reinforcement learning | Final selected model after evaluation |

The agent learns from historical trading data rather than following manually defined buy and sell rules.

## Features

- Historical market-data retrieval and preparation.
- Reinforcement-learning trading environment.
- Long and short trading decisions.
- Technical-indicator analysis.
- Comparison of DQN, A2C, and PPO.
- Stable-Baselines3-based model training.
- Random train/test/evaluation experiments.
- Model loading and later evaluation workflows.
- Interactive Brokers trading-agent integration.
- Notebook-based research and experimentation workflow.

## Repository Structure

```text
.
├── Getting Historical Data.ipynb   # Retrieves and prepares historical market data
├── SB3_dqn_a2c_ppo_new10.ipynb     # Historical-data analysis and DQN/A2C/PPO comparison
├── load_v03.ipynb                  # Random train/test/evaluation workflow
├── load_v05.ipynb                  # Later model loading, training, and evaluation workflow
├── IBKR_TrainModel.ipynb           # Training workflow for the Interactive Brokers model
├── IBKR_RLTrader.ipynb             # Interactive Brokers reinforcement-learning trader
└── README.md
```

## Requirements

This repository does not currently include a central dependency file such as:

```text
requirements.txt
pyproject.toml
environment.yml
```

Before running the notebooks, create a Python environment and install the packages imported by the notebooks.

The project uses libraries related to:

- Jupyter Notebook
- Python data analysis
- Reinforcement learning
- Stable-Baselines3
- Technical analysis
- Hyperparameter optimization
- Interactive Brokers connectivity

The exact dependency versions should be determined from the import statements inside the notebooks.

## Installation

### 1. Clone the repository

```bash
git clone [https://github.com/mastorasg/aida_thesis.git](https://github.com/mastorasg/aida_thesis.git)
cd aida_thesis
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

### 3. Activate the environment

On Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

On Windows Command Prompt:

```cmd
.venv\Scripts\activate
```

On macOS or Linux:

```bash
source .venv/bin/activate
```

### 4. Install Jupyter

```bash
pip install jupyter
```

### 5. Install notebook dependencies

Open each notebook and review its import statements before execution.

Install the required packages using `pip`. For example:

```bash
pip install pandas numpy matplotlib jupyter
```

Install the reinforcement-learning, optimization, technical-analysis, and Interactive Brokers packages required by the specific notebooks.

> The repository does not currently provide one verified installation command for every dependency. Do not assume that packages or versions not imported by the notebooks are required.

### 6. Start Jupyter Notebook

```bash
jupyter notebook
```

Jupyter will open in your browser. From there, open the notebooks in the recommended order.

## Workflow

The project is organised as Jupyter notebooks rather than executable Python scripts.

A typical workflow is:

1. Open `Getting Historical Data.ipynb`.
2. Retrieve, inspect, and prepare the historical market data.
3. Open `SB3_dqn_a2c_ppo_new10.ipynb`.
4. Analyse the data and compare the DQN, A2C, and PPO models.
5. Use `load_v03.ipynb` for random train/test/evaluation experiments.
6. Use `load_v05.ipynb` for the later loading, training, and evaluation workflow.
7. Run `IBKR_TrainModel.ipynb` to train the model intended for the Interactive Brokers implementation.
8. Run `IBKR_RLTrader.ipynb` to load the trained agent and use the Interactive Brokers trading workflow.

> Run notebook cells in order. Later cells may depend on variables, files, trained models, or processed data created by earlier cells.

## Data Preparation

The data-preparation stage retrieves and processes historical market information for use by the reinforcement-learning environment.

The workflow may include:

- Loading historical market-price data.
- Cleaning missing or invalid values.
- Selecting date ranges.
- Calculating technical indicators.
- Creating the observation data used by the RL agent.
- Splitting data into training, testing, and evaluation periods.

The quality and time period of historical data have a major effect on model evaluation results.

## Reinforcement Learning Environment

The trading problem is represented as a reinforcement-learning environment.

At each time step, the agent:

1. Receives an observation of the market state.
2. Uses price information and technical indicators as input.
3. Selects a trading action.
4. Receives a reward based on the action's outcome.
5. Continues through the historical data.

The model learns through repeated interaction with historical data. The goal is to maximize cumulative reward according to the environment's reward definition.

## Model Evaluation

The project evaluates models using historical data and train/test/evaluation workflows.

Important considerations include:

- Training results alone do not prove that a strategy will work in the future.
- Backtesting results depend on the selected data, reward function, features, transaction-cost assumptions, and model parameters.
- Different market periods can produce different outcomes.
- Real trading introduces additional risks, including spreads, slippage, latency, liquidity constraints, partial fills, and changing market conditions.

## Interactive Brokers Integration

The final brokerage-platform workflow uses **Interactive Brokers**.

### Training

`IBKR_TrainModel.ipynb` contains the training workflow for the model intended for Interactive Brokers use.

### Trading agent

`IBKR_RLTrader.ipynb` contains the reinforcement-learning trader workflow. It is intended to load the trained model, prepare market observations, obtain an action from the agent, and use the Interactive Brokers integration for trading-related operations.

### OANDA code

Some OANDA-related code may remain in the repository as commented-out code from earlier experimentation. OANDA is not part of the final active implementation described by this repository.

## Safety and Paper Trading

Before attempting any broker connection or automated trading:

- Use an Interactive Brokers paper-trading account.
- Verify that TWS or IB Gateway is configured correctly.
- Check the selected account, client ID, host, port, and market-data permissions.
- Confirm order sizes and position limits.
- Add stop conditions and risk-management limits.
- Inspect generated orders before sending them.
- Test the workflow with non-live data whenever possible.
- Never place credentials, account numbers, API keys, or configuration secrets in Git commits.

## Limitations

This repository is a research and educational project. It has important limitations:

- Historical results do not guarantee future performance.
- Reinforcement-learning agents can overfit historical data.
- Financial markets change over time.
- Backtest performance can differ from live-trading performance.
- Transaction costs, spreads, and slippage can significantly affect results.
- External broker systems can fail or behave differently from local tests.
- The agent may make losing decisions, including repeated losses during unexpected market conditions.

## Future Improvements

Possible future improvements include:

- Adding a `requirements.txt` file with pinned dependency versions.
- Adding a reproducible environment configuration.
- Adding automated tests for data processing and trading logic.
- Adding clearer notebook execution instructions.
- Adding experiment tracking and model-version tracking.
- Adding detailed risk-management rules.
- Including slippage and liquidity modelling in evaluation.
- Adding walk-forward validation.
- Evaluating more assets and market conditions.
- Running longer paper-trading experiments before any live deployment.
- Separating reusable code from notebooks into Python modules.

## Thesis Reference

Mastoras, G. (2025). *Reinforcement Learning-Based Stock Trading: Training Evaluation and Integration of an Agent into a Brokerage Platform Bot*. Master's Thesis, Department of Applied Informatics, University of Macedonia.

Thesis link:

https://dspace.lib.uom.gr/bitstream/2159/33294/1/MastorasGeorgiosMsc2025.pdf

## Disclaimer

This repository is provided for educational, academic, and experimental purposes only.

Nothing in this repository should be interpreted as financial, investment, legal, or tax advice. Automated trading carries substantial risk. Use paper trading, independent testing, and appropriate risk controls before considering any real-money trading.
