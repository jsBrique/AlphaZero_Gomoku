## AlphaZero-五子棋
这是AlphaZero算法的实现，用于从纯粹的自我训练，从训练中玩一种简单的棋盘游戏Gomoku（也称为五子棋）。 Gomoku游戏比围棋或国际象棋要简单得多，因此我们可以专注于AlphaZero的训练计划，并在几小时内在单台PC上获得相当不错的AI模型。

参考:  
1. AlphaZero: Mastering Chess and Shogi by Self-Play with a General Reinforcement Learning Algorithm
2. AlphaGo Zero: Mastering the game of Go without human knowledge

### 更新2018.1.17: 现在支持使用PyTorch训练!

### 不同模型数据的对比效果
- 400次MCTS搜索的模型效果:

![playout400](https://raw.githubusercontent.com/junxiaosong/AlphaZero_Gomoku/master/playout400.gif)

- 800次MCTS搜索的模型效果:  
![playout800](https://raw.githubusercontent.com/junxiaosong/AlphaZero_Gomoku/master/playout800.gif)

### 依赖库
如果只是使用已经训练好的模型，只需安装以下依赖:
- Python >= 2.7
- Numpy >= 1.11

从头开始训练AI，需要这些依赖:
- Theano >= 0.7 and Lasagne >= 0.1      
or
- PyTorch >= 0.2.0

**PS**: 如果你的Theano的版本 > 0.7, 请从这里 [issue](https://github.com/aigamedev/scikit-neuralnetwork/issues/235) 安装Lasagne,  
另外, 强制使用pip降级Theano至0.7 命令：``pip install --upgrade theano==0.7.0``

如果您想使用其他DL框架（如TensorFlow或MXNet）来训练模型，则只需重写policy_value_net.py。

### Getting Started
直接使用已经训练好的模型游玩, 只需在程序目录下运行这个脚本:  
```
python human_play.py  
```
您可以修改human_play.py以尝试不同的提供模型或纯粹的MCTS。

为了从头开始训练AI模型，利用Theano和Lasagne直接运行： 
```
python train.py
```
使用PyTorch，首先修改文件 [train.py](https://github.com/junxiaosong/AlphaZero_Gomoku/blob/master/train.py), i.e., 注释该行
```
from policy_value_net import PolicyValueNet  # Theano and Lasagne
```
并取消注释该行
```
# from policy_value_net_pytorch import PolicyValueNet  # Pytorch
```
然后执行: ``python train.py``  (使用GPU训练, 修改 ``use_gpu=True``)

模型（best_policy.model和current_policy.model）将在每次更新时保存（默认为50）。

**训练提示:**
1. 从6 * 6板开始并连续4次是很好的做法。 对于这种情况，我们可能会在约2个小时内在500〜1000个自我游戏中获得相当不错的效果。
2. 对于8 * 8电路板和连续5个电路板的情况，可能需要2000〜3000个自我玩游戏来获得一个好的模型，并且在一台PC上可能需要2天左右的时间。

### 拓展阅读
该项目作者在知乎专栏的文章中描述了有关该项目的一些细节: [https://zhuanlan.zhihu.com/p/32089487](https://zhuanlan.zhihu.com/p/32089487) 
