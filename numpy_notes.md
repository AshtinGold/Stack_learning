# Numpy learning notes for all

Mastering numpy means mastering its vector manipulation operations that are abundant in AI today, where deep learning is essentially a rebrand of linear algebra, performed in the stochastic sense.

Q: I have a single-channel mask. How tdo I apply it to an RGB image?  
A: `mask_3d = medsam_seg[:, :, None] * np.ones(3, dtype=int)[None, None, :]`

Q: 
