# AlphaZero Gomoku - Enhanced Setup

## Overview
This is an enhanced setup of the AlphaZero Gomoku implementation with fixes for modern PyTorch compatibility and support for custom board configurations.

## Fixed Issues
- Updated PyTorch API calls to be compatible with modern PyTorch versions
- Fixed deprecated `loss.data[0]` and `entropy.data[0]` calls to use `.item()` instead
- Fixed deprecated `log_softmax` calls to include `dim` parameter
- Addressed tensor creation warnings

## Answers to Your Questions

### 1. What does `python train.py` actually do, what's the default option?

The `train.py` script implements the complete AlphaZero training pipeline for Gomoku:

**Default Options:**
- Board size: 6x6
- Win condition: 4 in a row
- Training episodes: 1500 game batches
- MCTS playouts: 400 simulations per move
- Learning rate: 2e-3
- Batch size: 512
- Network architecture: Convolutional neural network with policy and value heads

**What it does:**
1. Creates a neural network (Policy-Value Net) to evaluate board positions
2. Runs self-play games using MCTS to generate training data
3. Trains the network on the self-play data using reinforcement learning
4. Evaluates the trained model periodically against a pure MCTS player
5. Saves the best performing model

### 2. If I want to train a 12x12, 5 in a row model, is it feasible?

**Yes, it's feasible!** I've created a custom training script that supports this:

```bash
# Train on 12x12 board with 5 in a row to win
python train_custom.py --width 12 --height 12 --n_in_row 5

# Train on 8x8 board with 5 in a row to win (faster alternative)
python train_custom.py --width 8 --height 8 --n_in_row 5

# Use GPU acceleration if available
python train_custom.py --width 12 --height 12 --n_in_row 5 --use_gpu
```

**Important considerations for 12x12, 5-in-a-row:**
- Significantly more computational resources required
- Much longer training time (potentially weeks)
- Larger neural network needed (due to bigger board)
- More memory usage
- You may need to adjust hyperparameters:
  - Reduce batch_size if running out of memory
  - Increase n_playout for stronger play but slower training
  - Adjust learning rate as needed

### 3. Does `train.py` use the modern graphics card (CUDA) efficiently?

**Current Status:**
- The original code has CUDA support (`use_gpu=True` parameter)
- However, it uses older PyTorch paradigms that may not be fully optimized
- The code has been updated to work with modern PyTorch but could be further optimized

**To enable GPU usage:**
```bash
# For the original training
python train.py --use_gpu  # (after modifying the main script to accept this argument)

# For the custom training
python train_custom.py --width 8 --height 8 --n_in_row 5 --use_gpu
```

**Potential optimizations for better GPU utilization:**
- Use larger batch sizes when possible
- Implement mixed precision training
- Optimize data loading pipelines
- The current implementation works but could be enhanced for better GPU efficiency

## How to Run Different Configurations

### Quick Test (Small Board)
```bash
cd /home/xinchengo/repo/AlphaZero_Gomoku
. .venv/bin/activate
python test_game.py
```

### Standard Training (6x6, 4-in-a-row)
```bash
python train.py
```

### Custom Training (e.g., 8x8, 5-in-a-row)
```bash
python train_custom.py --width 8 --height 8 --n_in_row 5
```

### Large Board Training (12x12, 5-in-a-row)
```bash
python train_custom.py --width 12 --height 12 --n_in_row 5 --use_gpu
```

### Play Against Pre-trained Model
```bash
python human_play.py
```

## Notes on Training Large Boards

For training on larger boards like 12x12:
1. **Start small**: Begin with 6x6 or 8x8 to validate your setup
2. **Resource planning**: Large boards require significantly more memory and compute
3. **Time expectations**: Training can take days or weeks for complex configurations
4. **Consider curriculum learning**: Train on smaller boards first, then transfer knowledge

## Troubleshooting

If you encounter memory issues:
- Reduce `batch_size` in the training parameters
- Reduce `n_playout` for faster but potentially weaker MCTS
- Use a machine with more RAM/GPU memory

If you encounter CUDA errors:
- Check that your PyTorch version supports your GPU
- Try running without `--use_gpu` flag to use CPU instead