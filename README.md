###AlphaZero，五子棋
这是AlphaZero算法的实现，用于从纯粹的自我演奏训练中玩简单的棋盘游戏Gomoku（也称为五子棋或五人一组）。Gomoku游戏比Go或国际象棋要简单得多，因此我们可以专注于AlphaZero的训练计划，并在几小时内在单台PC上获得相当不错的AI模型。

参考文献：

AlphaZero：使用通用强化学习算法通过自我掌握棋和棋
AlphaGo Zero：在没有人类知识的情况下掌握Go的游戏
###更新2018.1.17：现在支持使用PyTorch进行培训！
训练模型之间的示例游戏
每次移动400次播放：
playout400
每次移动800个播放：
playout800
##要求
要使用训练有素的AI模型，只需要：

Python> = 2.7
Numpy> = 1.11
为了从头开始训练AI模型，还需要：

Theano> = 0.7，千层面> = 0.1 
或
PyTorch> = 0.2.0
PS：如果你的Theano的版本> 0.7，请按照这个问题安装千层面，
否则，强制点将Theano降级到0.7pip install --upgrade theano==0.7.0

如果您想使用其他DL框架（如TensorFlow或MXNet）来训练模型，则只需重写policy_value_net.py。

##入门
要使用提供的模型进行游戏，请从目录运行以下脚本：

python human_play.py  
您可以修改human_play.py以尝试不同的提供模型或纯粹的MCTS。

为了从头开始培训AI模型，Theano和Lasagne直接运行：

python train.py
使用PyTorch，首先修改文件train.py，即注释该行

from policy_value_net import PolicyValueNet  # Theano and Lasagne
并取消注释该行

# from policy_value_net_pytorch import PolicyValueNet  # Pytorch
然后执行:( python train.py 使用GPU训练，设置use_gpu=True）

模型（best_policy.model和current_policy.model）将在每次更新时保存（默认为50）。

##训练提示：

从6 * 6板开始并连续4次是很好的做法。对于这种情况，我们可能会在约2个小时内在500〜1000个自我游戏中获得相当不错的模式。
对于8 * 8电路板和连续5个电路板的情况，可能需要2000〜3000个自我玩游戏来获得一个好的模型，并且在一台PC上可能需要2天左右的时间。
##进一步阅读
我的文章描述了有关中文实施的一些细节：https : //zhuanlan.zhihu.com/p/32089487
