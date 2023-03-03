---
title: 'Generative Adversarial Networks (GANs)'
date: '2023-03-03'
tags: ['machine_learning', 'ai']
---

![](/static/images/gans/gans.jpeg)

## Introduction

Generative Adversarial Networks (GANs) are a type of neural network architecture that have gained a lot of attention in recent years. GANs are a type of deep learning model that can produce new and original data. They are fundamentally different in their aim. and methods to CNNs for classification, segmentation or object detection. GANs have initially not been meant to be an image analysis tool, but to produce naturally looking images. As the technology advances, it also becomes increasingly important to consider the potential implications of using GANs. In this blog post, we will discuss what GANs are, how they work, some of their applications, limitations, ethical considerations, and the impact of GANs on society.

## How GANs Work

GANs consist of two neural networks that work together in a game-like setting - called minimax game. In such game, both players have access to the same variables, but have opposing goals, so that they will manipulate the variables in different directions. The first network is the generator, which generates new data samples. The second network is the discriminator, which evaluates the generated samples and determines whether they are real or fake. The generator tries to produce realistic samples that can fool the discriminator, while the discriminator tries to correctly identify the real samples from the fake ones. This process continues iteratively, with the generator improving its ability to create realistic samples and the discriminator becoming better at identifying fake samples. While at first glimpse this does not sound much different from any loss function, which in turn compares the generated output from the model, with the actual de-facto output, there exists a fundamental difference. **_A loss function is “static”, but the “judge” or “discriminator” network part is trainable._**

![Untitled](/static/images/gans/gan1.png)

_Figure 1. Fundamental GAN setup for image generation consisting of Generator and Discriminator networks_

From the figure 2 we can see the generative part in orange color, where random numbers are drawn from the latent space and, are converted to a set of fake images, by generator network. Parallel to that, from the database of real images, **the source of truth,** a matching number of examples is randomly drawn. Both the generated fake images and the real images are fed into the discriminator. The discriminator CNN takes the batch of real and fake images and decides for each if it appears real (yielding a value close to “1”) or fake (”0”).

![Untitled](/static/images/gans/gan2.png)

_Figure 2. Generator (orange) creates fake images based on random numbers drawn from a latent space. These together with the set of randomly drawn real images are fed in batches into the discriminator CNN._

Error is then calculated on the number of correct assignments the discriminator can do on the batch of generated and real images. Both type of networks can update their respective parameters based on the error signal.

## Applications of GANs

GANs have been used in a variety of applications, including image and video generation, data augmentation, and style transfer. One of the most impressive applications of GANs is in image generation, where the generator can create realistic images that are difficult to distinguish from real images. This has potential applications in the entertainment industry, such as creating realistic special effects in movies and video games. GANs can also be used for data augmentation in machine learning, where they can generate new data samples to increase the size of the training set. Another application of GANs is style transfer, where the style of one image can be transferred to another image. This can be used for artistic purposes, such as creating new versions of paintings in the style of famous artists. For the generator, the ultimate goal is to **maximize** the error, since this signals that it has successfully fooled discriminator into taking fake images for real. On the other hand, the discriminator goal is to **minimize the error,** indicating its’ success in telling true and fake examples apart.
Examples of applications of GANs are the following:

### Generating examples for image datasets

Generating new plausible samples was the application described in the original paper by Ian Goodfellow, et al. in the 2014 paper [“Generative Adversarial Networks”](https://arxiv.org/pdf/1406.2661) where GANs were used to generate new plausible examples for the MNIST handwritten digit dataset, the CIFAR-10 small object photograph dataset, and the Toronto Face Database.

![Untitled](/static/images/gans/gans-image-dataset.png)

### Generate Photographs of Human Faces

ero Karras, et al. in their 2017 paper titled ["Progressive Growing of GANs for Improved Quality, Stability, and Variation”](https://arxiv.org/abs/1710.10196) demonstrate the generation of plausible realistic photographs of human faces. They are so real looking, in fact, that it is fair to call the result remarkable. As such, the results received a lot of media attention. The face generations were trained on celebrity examples, meaning that there are elements of existing celebrities in the generated faces, making them seem familiar, but not quite.

![Untitled](/static/images/gans/gans-image-2.png)

### Generate Realistic Photographs

Andrew Brock, et al. in their 2018 paper titled [“Large Scale GAN Training for High Fidelity Natural Image Synthesis”](https://arxiv.org/abs/1809.11096) demonstrate the generation of synthetic photographs with their technique BigGAN that are practically indistinguishable from real photographs.

![Untitled](/static/images/gans/gans-image-3.png)

## Limitations of GANs

While GANs have shown impressive results in generating realistic data, they also have some limitations. One of the major limitations is the difficulty in training them. GANs require a large amount of data and computational resources to train effectively. Additionally, GAN training can be unstable, with the generator and discriminator often falling into a stalemate. Another limitation of GANs is the lack of control over the generated data. While GANs can generate realistic data, they do not allow for fine-grained control over the generated samples. Some reasons why GAN training might fail are:

- **Mode Dropping** - is the phenomenon in forward KL (Kullback-Leibler) divergence caused by regions of data distributions not being covered by the generator distribution. This drives forward KL to infinity and punishes the generator for not including the entire data distribution.
- **Poor Convergence** - caused in cases where the discriminator network learns too early to distringuish between real and fake examples - which will very likely happen during entire training time of the GAN.

## Future of GANs

The potential applications of GANs are vast, and there is ongoing research in this field to improve the performance and capabilities of GANs. One area of research is in improving the stability of GAN training, which can be difficult due to the game-like setting of the generator and the discriminator. Another area of research is in developing GANs that can generate more diverse and complex data, such as 3D objects and natural language. With continued research and development, the capabilities of GANs will only continue to grow.

## Ethical Considerations

As with any technology, GANs also raise ethical considerations. One of the main concerns is the potential for GANs to be used for malicious purposes, such as creating fake images or videos for propaganda or misinformation. Additionally, GANs could be used to create deepfakes, which are manipulated videos that can be difficult to distinguish from real videos. Another ethical concern is the potential for GANs to perpetuate biases in the data they are trained on. If the training data contains biased information, the GANs may learn and perpetuate those biases in the generated data.

It is important for developers and researchers to be aware of the ethical implications of their work and to consider the potential risks and benefits of their technologies. One way to mitigate the potential negative impacts of GANs is to establish ethical guidelines and policies for their use.

## Impact of GANs on Society

The use of GANs has the potential to impact society in many ways, both positive and negative. One potential positive impact is in the entertainment industry, where GANs can be used to create realistic special effects in movies and video games. Additionally, GANs can be used to create art and music that would be difficult for humans to create. Another potential positive impact is in healthcare, where GANs can be used to generate synthetic data for medical research and drug development.

However, the use of GANs can also have negative impacts on society. One concern is the potential for GANs to be used to create manipulated images and videos for propaganda or misinformation. Additionally, the use of GANs could lead to the loss of jobs in industries such as graphic design and music composition. As with any technology, it is important to consider the potential impact of GANs on society and to work towards minimizing any negative impacts.

## Conclusion

Generative Adversarial Networks are a promising area of research in artificial intelligence, with a wide range of applications in various industries. While GANs have limitations and ethical considerations, continued research and development can help mitigate these concerns. The potential for GANs to generate new and original data is exciting, and we can expect to see even more impressive applications of GANs in the future. As the technology advances, it is important for developers and researchers to consider the potential impacts of GANs on society and to work towards ensuring that their use is ethical and beneficial for all.
