# TokenLearner: What Can 8 Learned Tokens Do for Images and Videos?

<div align="center">
  <img src="https://blogger.googleusercontent.com/img/a/AVvXsEiylT3_nmd9-tzTnz3g3Vb4eTn-L5sOwtGJOad6t2we7FsjXSpbLDpuPrlInAhtE5hGCA_PfYTJtrIOKfLYLYGcYXVh1Ksfh_C1ZC-C8gw6GKtvrQesKoMrEA_LU_Gd5srl5-3iZDgJc1iyCELoXtfuIXKJ2ADDHOBaUjhU8lXTVdr2E7bCVaFgVHHkmA=s1600"><br>
  <small>Source: <a href="https://ai.googleblog.com/2021/12/improving-vision-transformer-efficiency.html">Improving Vision Transformer Efficiency and Accuracy by Learning to Tokenize</a></small>
</div><br>

A TensorFlow implementation of TokenLearner: What Can 8 Learned Tokens Do for Images and Videos? [1]. In this paper, an earlier version of which is presented at NeurIPS 2021 [2], the authors suggest an adaptive token learning algorithm that makes ViT computationally much more efficient (in terms of FLOPs) and also increases downstream accuracy (here classification accuracy). Experimenting with CIFAR-10 we reduce the number of pathces from **64** to **4** (number of adaptively learned tokens) and also report a boost in the accuracy. We experiment with different hyperparameters and report results which aligns with the literature.

## With and Without TokenLearner

We report results training our mini ViT with and without the vanilla TokenLearner module here. 
You can find the vanilla Token Learner module in the [`TokenLearner.ipynb`](https://github.com/ariG23498/TokenLearner/blob/master/TokenLearner.ipynb) notebook.

| **TokenLearner** | **# tokens in<br> TokenLearner** | **Top-1 Acc<br>(Averaged across 5 runs)** | **TensorBoard** |
|:---:|:---:|:---:|:---:|
| N | - | 56.112% | [Link](https://tensorboard.dev/experiment/vkCwM49dQZ2RiK0ZT4mj7w/) |
| Y | 8 | **56.55%** | [Link](https://tensorboard.dev/experiment/vkCwM49dQZ2RiK0ZT4mj7w/) |
| N | - | 56.37% | [Link](https://tensorboard.dev/experiment/hdyJ4wznQROwqZTgbtmztQ/) |
| Y | 4 | **56.4980%** | [Link](https://tensorboard.dev/experiment/hdyJ4wznQROwqZTgbtmztQ/) |
| N | - (# Transformer layers: 8) | 55.36% | [Link](https://tensorboard.dev/experiment/sepBK5zNSaOtdCeEG6SV9w/) |

## TokenLearner v1.1

We have also implemented the Token Learner v11 module which aligns with the [official implementation](https://github.com/google-research/scenic/blob/main/scenic/projects/token_learner/model.py). The Token Learner v11 module can be found in the [`TokenLearner-V1.1.ipynb`](https://github.com/ariG23498/TokenLearner/blob/master/TokenLearner-V1.1.ipynb) notebook. The results training with this module are as follows:

| **# Groups** | **# Tokens** | **Top-1 Acc** | **TensorBoard** |
|:---:|:---:|:---:|:---:|
| 4 | 4 | 54.638% | [Link](https://tensorboard.dev/experiment/KmfkGqAGQjikEw85phySmw/) |
| 8 | 8 | 54.898% | [Link](https://tensorboard.dev/experiment/0PpgYOq9RFWV9njX6NJQ2w/) |
| 4 | 8 | 55.196% | [Link](https://tensorboard.dev/experiment/WUkrHbZASdu3zrfmY4ETZg/) |  

We acknowledge that the results with this new TokenLearner module are slightly off than expected and this might
mitigate with hyperparameter tuning.

# Acknowledgements

- [Michael S. Ryoo](http://michaelryoo.com/): The first author of the paper.
- [Google Developers Experts Program](https://developers.google.com/programs/experts/) and [JarvisLabs.ai](https://jarvislabs.ai/) for providing credits to perform extensive experimentation on A100 GPUs.


# References

[1] TokenLearner: What Can 8 Learned Tokens Do for Images and Videos?; Ryoo et al.; arXiv 2021; https://arxiv.org/abs/2106.11297

[2] TokenLearner: Adaptive Space-Time Tokenization for Videos; Ryoo et al., NeurIPS 2021; https://openreview.net/forum?id=z-l1kpDXs88
