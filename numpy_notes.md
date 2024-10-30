# Numpy learning notes for all

Mastering numpy means mastering its vector manipulation operations that are abundant in AI today, where deep learning is essentially a rebrand of linear algebra, performed in the stochastic sense.

Q: I have a single-channel mask. How tdo I apply it to an RGB image?  
A: An obvious way is to create a 3D mask. A fast effective way to do it is by this code:  
`mask_3d = seg_mask[:, :, None] * np.ones(3, dtype=int)[None, None, :]`
Here we basically use a cartesian operation while ensuring dimensions do not overlap, effectively broadcasting our original segmentation mask into 3D.  
Most likely you will need to do `255 - img` to invert the color at the end.

Q: TypeError: Cannot handle this data type: (1, 1, 3), <f4  
A: The error message seems to be complaining about the shape, but it is really about the data type. The issue is with the float (0–1) type of the array. Convert the array to Uint (0–255).

`im = Image.fromarray((x * 255).astype(np.uint8))`
