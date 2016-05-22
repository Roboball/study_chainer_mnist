##�T�v

�[�w�w�K�̃t���[�����[�N Chainer �� MNIST ���g�����T���v���X�N���v�g�������Ă݂܂����B

���̃T���v���� MNIST �Ƃ����菑����0�`9�̐����𕪗ނ��邽�߂̑��w�p�[�Z�v�g���� (MLP) �̎�����Ȃ�ł����A�R�[�h�\���������ƒ��߂Ă��邤���Anet.py ���g������΁A�ʂ̕����ɕύX�ł������Ȃ��ƂɋC���t���܂����B

����́A���w�p�[�Z�v�g���� (MLP) �ɉ����āA�P���p�[�Z�v�g���� (SP)�Ə�ݍ��݃j���[�����l�b�g���[�N (CNN) ��ǉ����܂����B�����āAtrain_mnist.py ���W���o�͂ɕ\������e epoch ���Ƃ� "accuracy" �� "loss" �̐��ڂ��r���Ă݂܂����B

##MNIST�T���v��

���񎎂��� MNIST �T���v����[������](https://github.com/pfnet/chainer/tree/master/examples/mnist)�ɂ���܂��B

�d�v�ȃX�N���v�g�͈ȉ��̒ʂ�ł��B

|�X�N���v�g|�T�v|
|:--|:--|
|data.py|MNIST�̃f�[�^�Z�b�g��ǂݍ��ށB�茳�Ƀf�[�^�Z�b�g���Ȃ��Ƃ��̓l�b�g����_�E�����[�h����B|
|net.py|�j���[�����l�b�g���[�N�̃N���X���`����B|
|train_mnist.py|MNIST�̃f�[�^�Z�b�g�� net.py �̃j���[�����l�b�g���[�N�Ŋw�K����B|

##�g�p�����j���[�����l�b�g���[�N

MNIST �T���v���ɕt���� net.py �� SP �� CNN �p�̃N���X��ǉ����܂����B

```python
import chainer
import chainer.functions as F
import chainer.links as L

class MnistMLP(chainer.Chain):

    """An example of multi-layer perceptron for MNIST dataset.

    This is a very simple implementation of an MLP. You can modify this code to
    build your own neural net.

    """
    def __init__(self, n_in=784, n_units=1000, n_out=10):
        super(MnistMLP, self).__init__(
            l1=L.Linear(n_in, n_units),
            l2=L.Linear(n_units, n_units),
            l3=L.Linear(n_units, n_out),
        )

    def __call__(self, x):
        h1 = F.relu(self.l1(x))
        h2 = F.relu(self.l2(h1))
        return self.l3(h2)

# �����܂ŃI���W�i���̂܂܁B

# ��������ǉ������N���X

class MnistSP(chainer.Chain):

    """An example of simple perceptron for MNIST dataset.

    """
    def __init__(self, n_in=784, n_out=10):
        super(MnistSP, self).__init__(
            l1=L.Linear(n_in, n_out),
        )

    def __call__(self, x):
        # param x --- chainer.Variable of array
        return self.l1(x)

class MnistCNN(chainer.Chain):

    """An example of convolutional neural network for MNIST dataset.
       refered page:
       http://ttlg.hateblo.jp/entry/2016/02/11/181322

    """

    def __init__(self, channel=1, c1=16, c2=32, c3=64, f1=256, \
                 f2=512, filter_size1=3, filter_size2=3, filter_size3=3):
        super(MnistCNN, self).__init__(
            conv1=L.Convolution2D(channel, c1, filter_size1),
            conv2=L.Convolution2D(c1, c2, filter_size2),
            conv3=L.Convolution2D(c2, c3, filter_size3),
            l1=L.Linear(f1, f2),
            l2=L.Linear(f2, 10)
        )

    def __call__(self, x):
        # param x --- chainer.Variable of array

        # �ȉ��̂悤�ȕϊ����K�v
        x.data = x.data.reshape((len(x.data), 1, 28, 28))

        h = F.relu(self.conv1(x))
        h = F.max_pooling_2d(h, 2)
        h = F.relu(self.conv2(h))
        h = F.max_pooling_2d(h, 2)
        h = F.relu(self.conv3(h))
        h = F.max_pooling_2d(h, 2)
        h = F.dropout(F.relu(self.l1(h)))
        y = self.l2(h)
        return y


```

Convolution2D �̓��͂��킩��ɂ��������B

�w�K���s���X�N���v�g train_mnist.py �͎g�p�����j���[�����l�b�g���[�N�̃O���t�f�[�^�� dot �`���ŏo�͂��Ă���܂��Bgraphviz �� PNG �ɕϊ����܂����B�����N���Ƃ��܂��F

[MnistSP �̃O���t](graph.sp.png) 

[MnistMLP �̃O���t](graph.mlp.png) 

[MnistCNN �̃O���t](graph.cnn.png) 

## ����

�������肢���ƁAaccuracy (�����قǗǂ�)�ł� SP �� 0.93�AMLP �� 0.98�ACNN �� 0.99�B
loss (�Ⴂ�قǗǂ�)�ł� SP �� 0.26�AMLP �� 0.1�ACNN �� 0.05�B

�Ƃ����킯�� MNIST �̎菑�������̔F���ɂ����āA���񌟏؂������ł� CNN ���ł��D�ꂽ�������Ƃ������Ƃ��m�F�ł��܂����B

![accuracy](fig_accuracy.png)
![loss](fig_loss.png)

## �����N
[Chainer](http://chainer.org/)

[CNN�̎����ŎQ�l�ɂ����y�[�W](http://ttlg.hateblo.jp/entry/2016/02/11/181322)

[�R�[�h�͂�����ɂ܂Ƃ߂Ă����Ă܂�](https://github.com/bunji2/study_chainer_mnist)