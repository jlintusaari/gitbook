# Color spaces

### HSV

Hue tells the color. Saturation is how pure the color is or how much there is color in the surface as opposed to gray. Technically it is the maximum difference in RGB channel values, with low values resulting in shades of gray determined by value. Value makes the whole thing brighter or darker.

![The hue and the value is approximately the same for the red color but saturation is different. ](../.gitbook/assets/image%20%283%29.png)

Note that with max saturation and value the color is as bright as it can be. [With saturation 0 and max value we get white](https://stackoverflow.com/questions/48109650/how-to-detect-two-different-colors-using-cv2-inrange-in-python-opencv) \(there is no color in it but it's maximally bright\). Value to 0 takes it to black.

### YCpCr

Y component contains the gray scale image. Link asking for [intuition](https://dsp.stackexchange.com/questions/4849/understanding-cb-and-cr-components-of-ycbcr-color-space) for Cp and Cr components, which encode the color. Used in video as eye is most sensitive to the Y component and Cp and Cr components can be compressed.

![From wikipedia. Public domain.](../.gitbook/assets/image%20%285%29.png)



