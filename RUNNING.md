# AlphaZero Gomoku Project Setup and Usage Guide

## Overview
This is an implementation of the AlphaZero algorithm for playing Gomoku (Five in a Row). The project has been successfully cloned and set up with dependencies.

## Environment Setup
- Created virtual environment using `uv venv`
- Installed dependencies: numpy, torch

## How to Run Different Components

### 1. Basic Game Test
```bash
cd /home/xinchengo/repo/AlphaZero_Gomoku
. .venv/bin/activate
python test_game.py
```
This runs a simple test between two AI players on a 4x4 board.

### 2. Human vs AI Game
```bash
cd /home/xinchengo/repo/AlphaZero_Gomoku
. .venv/bin/activate
python human_play.py
```
Note: This requires user input in the format "row,col" (e.g., "2,3") to make moves.

### 3. Training the Model
```bash
cd /home/xinchengo/repo/AlphaZero_Gomoku
. .venv/bin/activate
python train.py
```
Note: The training script has been modified to use PyTorch instead of Theano. There may be some compatibility issues with newer PyTorch versions, but the training does start successfully.

## Files Included
- `game.py`: Contains the Gomoku board and game logic
- `mcts_alphaZero.py`: Monte Carlo Tree Search implementation for AlphaZero
- `mcts_pure.py`: Pure MCTS implementation
- `human_play.py`: Interface for human vs AI gameplay
- `train.py`: Training pipeline
- `policy_value_net*.py`: Neural network implementations for different frameworks
- Pre-trained models: `best_policy_*.model`

## Known Issues
- The PyTorch version has some compatibility issues with newer PyTorch versions (deprecated methods)
- The human_play.py script requires manual input and cannot be run in automated environments
- The pre-trained models were created with Theano/Lasagne and may need conversion for PyTorch

## Requirements
- Python >= 3.6
- numpy
- torch (for PyTorch version)
- theano/lasagne (for original Theano version, though installation may fail on newer systems)