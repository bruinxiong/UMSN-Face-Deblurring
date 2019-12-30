# UMSN-Face-Deblurring
Deblurring Face Images using Uncertainty Guided Multi-Stream Semantic Networks

[Rajeev Yasarla](https://sites.google.com/view/rajeevyasarla/home), [Federico Perazzi](https://research.adobe.com/person/federico-perazzi/), [Vishal M. Patel](https://engineering.jhu.edu/ece/faculty/vishal-m-patel/)

[Paper Link](https://arxiv.org/pdf/1907.13106.pdf)

We propose a novel multi-stream architecture and training methodology that exploits semantic labels for facial image deblurring. The proposed Uncertainty Guided MultiStream Semantic Network (UMSN) processes regions belonging to each semantic class independently and learns to combine their outputs into the final deblurred result. Pixel-wise semantic labels are obtained using a segmentation network. A predicted confidence measure is used during training to guide the network towards challenging regions of the human face such as the eyes and nose. The entire network is trained in an endto-end fashion.

## Prerequisites:
1. Linux
2. Python 2 or 3
3. Pytorch version 0.4.1
4. CPU or NVIDIA GPU + CUDA CuDNN (CUDA 8.0)


## To test UMSN:
1. Download test datasets provided the authors of Ziyi et al.
    - https://sites.google.com/site/ziyishenmi/cvpr18_face_deblur
2. run test_data_generation.m
    - It renames the files counting from 1, for example 000001.png
3. python test_face_deblur.py --dataroot ./facades/github/ --valDataroot <path_to_test_data> --netG ./pretrained_models/Deblur_epoch_Best.pth

## To train UMSN:
1. Kernels are generated using,
     - [Boracchi and Foi, 2012]	Modeling the Performance of Image Restoration from Motion Blur Giacomo Boracchi and Alessandro Foi, Image Processing, IEEE Transactions on. vol.21, no.8, pp. 3502 - 3517, Aug. 2012,
     - 25000 kernels with size ranging from 13 to 29 are generated and saved as ".mat" file
2. Clean face images from Helen and CelebA are aligned and used as input to train UMSN 
3. python train_face_deblur.py --dataroot <path_to_train_data> --valDataroot ./facades/github/ --exp ./face_deblur --batchSize 10
    - input should be clean image. blurry images for training are generated by the code it self.

## To train Segmentation Netweork
Train Segmentation Netweork using the following command
1. training segmentation network with clean images,
    python seg_train.py --mode_clean 1 --dataroot ./facades/github/ --valDataroot ./facades/github/
2. training segmentation network with blurry images,
    python seg_train.py --mode_clean 0 --dataroot ./facades/github/ --valDataroot ./facades/github/
