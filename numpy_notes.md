# Numpy learning notes for all

Mastering numpy means mastering its vector manipulation operations that are abundant in AI today, where deep learning is essentially a rebrand of linear algebra, performed in the stochastic sense.

Q: I have a single-channel mask. How tdo I apply it to an RGB image?  
A: An obvious way is to create a 3D mask. A fast effective way to do it is by this code:  
`mask_3d = seg_mask[:, :, None] * np.ones(3, dtype=int)[None, None, :]`
Here we basically use a cartesian operation while ensuring dimensions do not overlap, effectively broadcasting our original segmentation mask into 3D.

Q: 
