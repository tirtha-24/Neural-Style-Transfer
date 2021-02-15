# NEURAL STYLE TRANSFER
Neural style transfer is an optimization technique used to take three images, a content image, a style reference image (such as an artwork by a famous painter), and the input/generated image we want to style -- and blend them together such that the input image is transformed to look like the content image, but “painted” in the style of the style image.

For the sake of implementation, we’ll take the base input image, a content image that we want to match, and the style image that we want to match. We’ll transform the base input image by minimizing the content and style distances (losses) with backpropagation, creating an image that matches the content of the content image and the style of the style image.

## HIGH LEVEL ARCHITECTURE
Neural style transfer uses a pretrained convolution neural network. Here, we use VGG-19. Then to define a loss function which blends two images seamlessly to create visually appealing art, NST defines the following inputs:
1. A content image (c) — the image we want to transfer a style to.
2. A style image (s) — the image we want to transfer the style from.
3. An input (generated) image (g) — the image that contains the final result (the only trainable variable).

![alt text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-2/architecture.jpeg)

In order to get both the content and style representations of our image, we will look at some intermediate layers within our model. As we go deeper into the model, these intermediate layers represent higher and higher order features. In this case, we are using the network architecture VGG19, a pretrained image classification network. These intermediate layers are necessary to define the representation of content and style from our images. For an input image, we will try to match the corresponding style and content target representations at these intermediate layers.

## LOSS FUNCTIONS
In this section we define two loss functions; the content loss function and the style loss function. The content loss function ensures that the activations of the higher layers are similar between the content image and the generated image. The style loss function makes sure that the correlation of activations in all the layers are similar between the style image and the generated image. We will be discussing the details below.

### CONTENT LOSS FUNCTION
The content cost function is making sure that the content present in the content image is captured in the generated image. It has been found that CNNs capture information about content in the higher levels, where the lower levels are more focused on individual pixel values. Therefore, we use the top-most CNN layer to define the content loss function.
Let A^l_{ij}(I) be the activation of the l th layer, i th feature map and j th position obtained using the image I. Then the content loss is defined as,

![alt_text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-2/content%20loss.png)

Essentially L_{content} captures the root mean squared error between the activations produced by the generated image and the content image.

**Intution**
If we visualise what is learnt by a neural network, there’s evidence that suggests that different feature maps in higher layers are activated in the presence of different objects. So if two images to have the same content, they should have similar activations in the higher layers.

### STYLE LOSS FUNCTION
Style information is measured as the amount of correlation present between features maps in a given layer. Next, a loss is defined as the difference of correlation present between the feature maps computed by the generated image and the style image. Mathematically, the style loss is defined as,

![alt_text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-2/style%20loss.png)

w^l (chosen uniform in this tutorial) is a weight given to each layer during loss computation and M^l is an hyperparameter that depends on the size of the l th layer.

The style matrix is essentially a Gram matrix, where the (i,j) th element of the style matrix is computed by computing the element wise multiplication of the i th and j th feature maps and summing across both width and height.

### FINAL LOSS

![alt_text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-2/final%20loss.png)

where α and β are user-defined hyperparameters.
By controlling α and β we can control the amount of content and style injected to the generated image.

## RESULT

### **CONTENT IMAGE**
![alt_text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-1/Green_Sea_Turtle_grazing_seagrass.jpg)

### **STYLE IMAGE**
![alt_text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-1/1024px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg)

### **GENERATED IMAGE**
![alt_text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-2/output1.png)



[**Reference**](https://towardsdatascience.com/light-on-math-machine-learning-intuitive-guide-to-neural-style-transfer-ef88e46697ee)
