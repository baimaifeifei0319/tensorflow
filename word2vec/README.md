# tf_word2vec

introduction: http://kexue.fm/archives/4402/

here we release a tf_word2vec. it use a new loss -- I called it random softmax loss.

一个较完整的tensorflow版本的word2vec封装，用了自己设计的loss降低训练计算量。



#word2vec_keras.py文件说明

上面是CBOW模型的代码，如果需要Skip-Gram，请自行修改，Keras代码这么简单，改起来也容易。

纵观代码，就会发现搭建模型的部分还不到10行。事实上，CBOW模型写起来是很简单的，唯一有难度的是为了提高效率而做的随机抽样版的softmax（随机选若干个目标做softmax，而不是完整softmax）。在Keras中，实现的方式就是手写Dense层，而不是用自带的Dense层。具体步骤是：1、通过random_uniform生成随机整数，也就是负样本id，然后跟目标输入拼在一起，构成一个抽样；2、通过Embedding层来存softmax的权重；3、把抽样中权重挑出来，组成一个小矩阵，然后用K后端做矩阵乘法，也就是实现抽样版本的Dense层了。反复看看代码就明白了。

最后，拼运行速度肯定拼不过Gensim版和原版的Word2Vec了，用Keras主要是灵活性强而已～这点大家需要留意哈。
转载到请包括本文地址：https://spaces.ac.cn/archives/4515
