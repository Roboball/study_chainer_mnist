# study_chainer_mnist

## �͂��߂�
Chainer �� MNIST ��p�������w�p�[�Z�v�g�����̃T���v�����������Ă݂�B

|�X�N���v�g|�T�v|�����̗L��|
|:--|:--|:--|
|data.py|MNIST�̃f�[�^�Z�b�g���擾����X�N���v�g|�Ȃ�|
|net.py|�j���[�����l�b�g���[�N���`����X�N���v�g�B�P���p�[�Z�v�g���� MnistSP�A���w�p�[�Z�v�g���� MnistMLP�A��ݍ��݃j���[�����l�b�g MnistCNN ���`����B|����|
|train_mnist.py|data.py �� net.py ���g�����w�K�p�X�N���v�g�B|����|


## train_mnist.py

- �������e

MNIST �̃f�[�^�Z�b�g���g���Ċw�K����B

- �R�}���h���C��

```
tran_mnist.py --net2 [sp|mlp|cnn]
```

--net2 �I�v�V������ǉ��B

|�l|�T�v|
|:--|:--|
|sp|�P���p�[�Z�v�g����|
|mlp|���w�p�[�Z�v�g����|
|cnn|��ݍ��݃j���[�����l�b�g|

- ���s��
```
\# train_mnist.py --net2 mlp
```

## classify.py

- �������e

0�`9 �̎菑�������̉摜�𕪗ނ���B

- �R�}���h���C��

```
Usage: classify.py [sp|mlp|cnn] model_path image_path
```

�������F�g�p����j���[�����l�b�g
�������Ftrain_mnist.py �ō쐬�������f���f�[�^�̃p�X
��O�����F���ޑΏۂƂȂ�菑�������̉摜�f�[�^�̃p�X

|�������̒l|�T�v|
|:--|:--|
|sp|�P���p�[�Z�v�g����|
|mlp|���w�p�[�Z�v�g����|
|cnn|��ݍ��݃j���[�����l�b�g|

- ���s��

```
\# python classify.py cnn model.cnn.npz number/four.png
input:  number/four.png
output:
        0: -14.180834
        1: 2.686594
        2: -2.928259
        3: -28.385714
        4: 12.872291
        5: -14.222157
        6: -5.834879
        7: -9.659436
        8: -16.648321
        9: -11.859789
class:  4
```

CNN �œ��͉摜�𕪗ނ������ʂ��u4�v�ł��邱�Ƃ������B
