## Image classification using LVMs on Product 650

This repo will classify common items on e-commerce website,

The original dataset is [Product 10K](https://www.kaggle.com/competitions/products-10k), with 141K images and amost 10K labels. I have choosen and labeled 650 detailed labels with roughly 1k original labels and 28K images and use it for benchmark.

Three different appoarchs will be employeed to classify images

- **[ResNet50](./ResNet.ipynb)** Accuracy: 83.82 (Augmented: 83.02)
- **[Vision Transformer](./ViT.ipynb)** *(ViT-base-patch-16)* Accuracy: 86.82 (Augmented: 86.89)
- **[CAFormer](https://arxiv.org/abs/2210.13452)**

  - *(caformer_s36_in21ft1k)* Accuracy: 87.55
  - *(caformer_b36_in21ft1k)* Accuracy: xx.xx
- **[FasterViT](https://arxiv.org/abs/2306.06189)**

  - *(fastervit_2_224)* Accuracy: 91.33
  - *(fastervit_3_224)* Accuracy: 91.87
- **[CLIP]()**

  - [Zero-shot](./CLIP-zeroshot.ipynb) Accuracy: 36.54
  - [Fine-tune](./CLIP-finetune.ipynb) Accuracy: 51.56

With **CLIP**, I believe there are plenty room for improvement, since I can only use `batch_size=32`, which means it can only proceed 1 samples with 32 class at a time. Increase the `batch_size` will significantly improve model performance.

You can map new labels to original dataset via [reduced_train.csv](./reduced_train.csv) and [reduced_test.csv](./reduced_test.csv)

### Device setting

Due to lack of resources, I am unable to load all of the image into one big giant dataset. SO I have to chunks it to multiple dataloaders.

There are other method for sampling on dataloader, and the most basic appoarch is to process items only when using it (process everything such as open image and `transform` in method `__getitem()__` of `Dataset`). However this method only efficent for few first epoch. Loading and transforming it cost roughly equivalent amount of time as training (even more if SSD speed is low). So I premake all the dataloader before, save it in `.pt` format, and it costs only few second for reading file from hard drive.
