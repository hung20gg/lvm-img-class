## Image classification using LVMs on Product 650

This repo will classify common items on e-commerce website,

The original dataset is [Product 10K](https://www.kaggle.com/competitions/products-10k), with 141K images and amost 10K labels. I have choosen and labeled 650 detailed labels with roughly 1k original labels and 28K images and use it for benchmark.

Three different appoarchs will be employeed to classify images

- **[ResNet50](./ResNet.ipynb)** Accuracy: 83.82 (Augmented: 83.02)
- **[Vision Transformer](./ViT.ipynb)** *(ViT-base-patch-16)* Accuracy: 86.82 (Augmented: 86.89)
- **[FasterViT](https://arxiv.org/abs/2306.06189)** *(fastervit_2_224)* Accuracy: 90.77 (still increasing)
- **[CLIP]()**
  - [Zero-shot](./CLIP-zeroshot.ipynb) Accuracy: 36.54
  - [Fine-tune](./CLIP-finetune.ipynb) Accuracy: 51.56

With **CLIP**, I believe there are plenty room for improvement, since I can only use `batch_size=32`, which means it can only proceed 1 samples with 32 class at a time. Increase the `batch_size` will significantly improve model performance.

You can map new labels to original dataset via [reduced_train.csv](./reduced_train.csv) and [reduced_test.csv](./reduced_test.csv)
