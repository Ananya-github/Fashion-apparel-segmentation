# Fashion-apparel-segmentation
Data[https://www.kaggle.com/c/imaterialist-fashion-2019-FGVC6]
Visual analysis of clothing is a topic that has received increasing attention in recent years. Being able to recognize apparel products and associated attributes from pictures could enhance the shopping experience for consumers, and increase work efficiency for fashion professionals.The goal of introducing a novel fine-grained segmentation task is joining forces between the fashion and computer vision communities. The proposed task unifies both categorization and segmentation of rich and complete apparel attributes, an important step toward real-world applications.

Object Instance Segmentation is an approach that gives us best of both worlds. It integrates object detection task where the goal is to detect object class along with bounding box prediction in an image and semantic segmentation task, which classifies each pixel into pre-defined categories Thus, it enables us to detect objects in an image while precisely segmenting a mask for each object instance.
Segmentation not only requires discrimination at pixel level but also a mechanism to project the discriminative features learnt at different stages of the encoder onto the pixel space.

1st model UNet:

The encoder is the first half in the architecture diagram . It is a pre-trained classification network like ResNet(VGG) where we apply convolution blocks followed by a maxpool downsampling to encode the input image into feature representations at multiple different levels.The decoder is the second half of the architecture. The goal is to semantically project the discriminative features (lower resolution) learnt by the encoder onto the pixel space (higher resolution) to get a dense classification. The decoder consists of upsampling and concatenation followed by regular convolution operations.

2nd model Mask-rcnn:

Mask R-CNN is a state of the art model for instance segmentation, developed on top of Faster R-CNN. Faster R-CNN is a region-based convolutional neural networks [2], that returns bounding boxes for each object and its class label with a confidence score.

To understand Mask R-CNN, let's first discus architecture of Faster R-CNN that works in two stages:

Stage1: The first stage consists of two networks, backbone (ResNet, VGG, Inception, etc..) and region proposal network. These networks run once per image to give a set of region proposals. Region proposals are regions in the feature map which contain the object.

Stage2: In the second stage, the network predicts bounding boxes and object class for each of the proposed region obtained in stage1. Each proposed region can be of different size whereas fully connected layers in the networks always require fixed size vector to make predictions. Size of these proposed regions is fixed by using either RoI pool (which is very similar to MaxPooling) or RoIAlign method.

Faster R-CNN predicts object class and bounding boxes. Mask R-CNN is an extension of Faster R-CNN with additional branch for predicting segmentation masks on each Region of Interest (RoI).In the second stage of Faster R-CNN, RoI pool is replaced by RoIAlign which helps to preserve spatial information which gets misaligned in case of RoI pool. RoIAlign uses binary interpolation to create a feature map that is of fixed size for e.g. 7 x 7. The output from RoIAlign layer is then fed into Mask head, which consists of two convolution layers. It generates mask for each RoI, thus segmenting an image in pixel-to-pixel manner.

3rd model Deepmac:

The idea of DeepMAC is based on MASK R-CNN. DeepMAC has shown significant performance improvement in creating instance masks of unknown objects. There are some differences between previous study like following:
1.Deeper and hourglass network as mask-heads.
2.Train late stage networks using not proposals of RPN but ground truth.

Output

![model_output](https://github.com/Ananya-github/Fashion-apparel-segmentation//blob/main/model_result.PNG?raw=true)

