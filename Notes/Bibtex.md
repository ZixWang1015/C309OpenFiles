### Here we introduce basic .bib file format to C309 teammates :>

## Latex论文引用习惯

.bib文件的修改：包含 @inproceedings和@article两大类。
- 其中，常见的对于国际上各类会议的引用都会采用@inproceedings类，它的.bib文件引用会包含五个部分，例如：非常著名的来自何凯明的MoCo论文，在CVPR上发表，我们就可以按下面格式来引用它。
  ``` bibtex
  @inproceedings{He2019MomentumCF,
  title={Momentum Contrast for Unsupervised Visual Representation Learning},
  author={Kaiming He and Haoqi Fan and Yuxin Wu and Saining Xie and Ross B. Girshick},
  booktitle={Proceedings of IEEE/CVF CVPR},
  year={2019},
  pages={9726-9735}
  }
  ```
  需要注意的是，非常著名的会议例如AAAI, CVPR, IEEE ICCV等，在booktitle中都会直接指名其缩写即可。
- 除此之外，我们经常需要引用期刊论文，例如我们非常熟悉的IEEE T-IFS，这类的引用就需要用到@article的开头了，而@article一般对应的是期刊，@inproceedings一般对应的是国际会议，期刊使用booktitle而会议使用journal，这些在修改我们的.bib文件时都需要注意。常见的@article的引用可以举个例子：
  ``` bibtex
  @article{liu2019socinf,
  title={Socinf: Membership inference attacks on social media health data with machine learning},
  author={Liu, Gaoyang and Wang, Chen and Peng, Kai and Huang, Haojun and Li, Yutong and Cheng, Wenqing},
  journal={IEEE Transactions on Computational Social Systems},
  volume={6},
  number={5},
  pages={907--921},
  year={2019},
  }
  ```
  与会议不同的是，期刊需要添加上volume和number, 并且温馨提示，不要忘了.bib文件中每个单元的英文逗号，缺少逗号会导致编译错误.

我们可以总结一下：
- 期刊论文：必须有卷号，期号，页码，年份；
- 会议论文：必须有年份，页码不做硬性要求

此外再强调一点，就是我们会统一将来自arxiv上的文章定义为@article，并且将其journal这一部分写作CoRR, arXiv: 20xx.xxxxx即可。
- 其引用格式可以参考这样的样式：
  ``` bibtex
  @article{liu2025longlladaunlockinglongcontext,
      title={LongLLaDA: Unlocking Long Context Capabilities in Diffusion LLMs}, 
      author={Xiaoran Liu and Zhigeng Liu and Zengfeng Huang and Qipeng Guo and Ziwei He and Xipeng Qiu},
      year={2025},
      journal={CoRR, arXiv:2506.14429},
      url={https://arxiv.org/abs/2506.14429}, # 这个可填可不填
  }
  ```
