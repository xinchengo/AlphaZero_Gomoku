## AlphaZero-Gomoku
This is an implementation of the AlphaZero algorithm for playing the simple board game Gomoku (also called Gobang or Five in a Row) from pure self-play training. The game Gomoku is much simpler than Go or chess, so that we can focus on the training scheme of AlphaZero and obtain a pretty good AI model on a single PC in a few hours.

References:
1. AlphaZero: Mastering Chess and Shogi by Self-Play with a General Reinforcement Learning Algorithm
2. AlphaGo Zero: Mastering the game of Go without human knowledge

### Update 2026: Modern PyTorch compatibility and custom board sizes!
### Update 2018.2.24: supports training with TensorFlow!
### Update 2018.1.17: supports training with PyTorch!

### Example Games Between Trained Models
- Each move with 400 MCTS playouts:
![playout400](https://raw.githubusercontent.com/junxiaosong/AlphaZero_Gomoku/master/playout400.gif)

### Requirements
To play with the trained AI models, only need:
- Python >= 3.6
- Numpy >= 1.11

To train the AI model from scratch, further need, either:
- Theano >= 0.7 and Lasagne >= 0.1 (may have compatibility issues with newer Python versions)
- PyTorch >= 1.0.0 (recommended, with modern compatibility fixes)
- TensorFlow

### Modern Updates
This fork includes several enhancements:
- Fixed compatibility issues with modern PyTorch versions
- Added support for custom board sizes (e.g., 12x12 with 5-in-a-row)
- Added GPU support with `--use_gpu` flag
- Improved error handling and documentation

### Getting Started

#### Virtual Environment Setup
```bash
# Create and activate virtual environment
uv venv
source .venv/bin/activate
# Install dependencies
uv pip install numpy torch
```

#### To play with provided models:
```bash
python human_play.py
```
You may modify human_play.py to try different provided models or the pure MCTS.

#### To train the AI model from scratch with PyTorch (recommended):
The train.py file has been updated to use PyTorch by default and includes modern PyTorch compatibility fixes.

For default 6x6 board with 4-in-a-row:
```bash
python train.py
```

For custom board sizes (e.g., 8x8 with 5-in-a-row):
```bash
python train_custom.py --width 8 --height 8 --n_in_row 5
```

For 12x12 board with 5-in-a-row:
```bash
python train_custom.py --width 12 --height 12 --n_in_row 5 --use_gpu
```

To use GPU acceleration (if available):
```bash
python train_custom.py --width 8 --height 8 --n_in_row 5 --use_gpu
```

#### Framework Selection
The train.py file is pre-configured to use PyTorch. If you want to use a different framework, modify the import statements:
```
# from policy_value_net import PolicyValueNet  # Theano and Lasagne
from policy_value_net_pytorch import PolicyValueNet  # Pytorch (default)
# from policy_value_net_tensorflow import PolicyValueNet # Tensorflow
```

The models (best_policy.model and current_policy.model) will be saved every a few updates (default 50).

**Note:** the 4 provided models were trained using Theano/Lasagne, to use them with PyTorch, please refer to [issue 5](https://github.com/junxiaosong/AlphaZero_Gomoku/issues/5).

**Tips for training:**
1. It is good to start with a 6 * 6 board and 4 in a row. For this case, we may obtain a reasonably good model within 500~1000 self-play games in about 2 hours.
2. For the case of 8 * 8 board and 5 in a row, it may need 2000~3000 self-play games to get a good model, and it may take about 2 days on a single PC.
3. For larger boards (e.g., 12x12), expect significantly longer training times and higher resource requirements.

### Further reading
My article describing some details about the implementation in Chinese: [https://zhuanlan.zhihu.com/p/32089487](https://zhuanlan.zhihu.com/p/32089487)
