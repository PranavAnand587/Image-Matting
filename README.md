# Image Matting with Bayesian and Knockout Matting

This project demonstrates the use of Bayesian Matting and Knockout Matting, techniques used to separate the foreground and background in images.

### Dependencies

- numpy
- cv2
- matplotlib

### Code Explanation

The main functions in this project are `bayesian_matting(compA, compB, backA, backB)` and `knockout_matting(compA, compB, backA, backB)`. These functions take in two composite images `(compA and compB)` and their corresponding background images `(backA and backB)`, and return the estimated foreground and alpha matte.

The functions first resize all images to have the same dimensions. They then calculate per-pixel foreground `F` and background `B` color estimates. The background color is adjusted to lie on the line between `F` and `B`. The alpha matte, which represents the transparency of the foreground, is then calculated and clipped to the range [0, 1]. Finally, the estimated foreground color is calculated.

### Usage

To use this code, you need to have two composite images and their corresponding background images. In this example, we use 'full_blue.jpg', 'full_violet.jpg', 'blue.jpg', and 'violet.jpg'. These images are read in, linearized, and then passed to the `bayesian_matting` and `knockout_matting` functions. The estimated foreground and alpha matte are then displayed.

```python

full_blue = plt.imread('full_blue.jpg')
full_violet = plt.imread('full_violet.jpg')
blue = plt.imread('blue.jpg')
violet = plt.imread('violet.jpg')

linear_full_blue = linearize(full_blue)
linear_full_violet = linearize(full_violet)
linear_blue = linearize(blue)
linear_violet = linearize(violet)

# Perform Bayesian Matting
estimated_foreground_bayesian, estimated_alpha_bayesian = bayesian_matting(linear_full_blue, linear_full_violet, linear_blue, linear_violet)

# Perform Knockout Matting
estimated_foreground_knockout, estimated_alpha_knockout = knockout_matting(linear_full_blue, linear_full_violet, linear_blue, linear_violet)

# Display the estimated foreground and alpha matte for Bayesian Matting
plt.imshow(cv2.cvtColor(estimated_foreground_bayesian, cv2.COLOR_BGR2RGB))
plt.title('Estimated Foreground (Bayesian Matting)')
plt.axis('off')
plt.show()

plt.imshow(estimated_alpha_bayesian, cmap='gray')
plt.title('Estimated Alpha Matte (Bayesian Matting)')
plt.axis('off')
plt.show()

# Display the estimated foreground and alpha matte for Knockout Matting
plt.imshow(cv2.cvtColor(estimated_foreground_knockout, cv2.COLOR_BGR2RGB))
plt.title('Estimated Foreground (Knockout Matting)')
plt.axis('off')
plt.show()

plt.imshow(estimated_alpha_knockout, cmap='gray')
plt.title('Estimated Alpha Matte (Knockout Matting)')
plt.axis('off')
plt.show()

```

