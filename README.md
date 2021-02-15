# NEURAL STYLE TRANSFER
Neural style transfer is an optimization technique used to take three images, a content image, a style reference image (such as an artwork by a famous painter), and the input/generated image we want to style -- and blend them together such that the input image is transformed to look like the content image, but “painted” in the style of the style image.

For the sake of implementation, we’ll take the base input image, a content image that we want to match, and the style image that we want to match. We’ll transform the base input image by minimizing the content and style distances (losses) with backpropagation, creating an image that matches the content of the content image and the style of the style image.

## HIGH LEVEL ARCHITECTURE
Neural style transfer uses a pretrained convolution neural network. Here, we use VGG-19. Then to define a loss function which blends two images seamlessly to create visually appealing art, NST defines the following inputs:
A content image (c) — the image we want to transfer a style to.
A style image (s) — the image we want to transfer the style from.
An input (generated) image (g) — the image that contains the final result (the only trainable variable).

![alt text](https://github.com/tirtha-24/Neural-Style-Transfer/blob/master/images-2/architecture.jpeg)

