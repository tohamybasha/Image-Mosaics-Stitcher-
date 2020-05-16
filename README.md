# Image-Mosaics-Stitcher

# 1 Getting correspondences
Use the provided code to get manually identified corresponding points from two views. “ginput” function provides an easy way to collect mouse click positions. The results will be sensitive to the accuracy of the corresponding points, when providing clicks, choose distinctive points in the image that appear in both views.

# 2 Computing the homography parameters
Write a function that takes a set of corresponding image points and computes the associated
3 3 homography matrix H. This matrix transforms any point p in one view to its correspond- ing homogeneous coordinates in the second view, pJ, such that pJ = Hp . Note that p and pJ are both 3D points in homogeneous coordinates. The function should take a list of n 4 pairs of corresponding points from the two views, where each point is specified with its 2D image coordinates. We can set up a solution using a system of linear equations Ax = b, where the 8 unknowns
of H are stacked into an 8-vector x , the 2n-vector b contains image points from one view, and
the 2n × 8 matrix A is filled appropriately so that the full system gives us λpJ = Hp . There
are only 8 unknowns in H because we set H3,3 = 1. Solve for the unknown homography matrix
parameters.
Verify that the homography matrix your function computes is correct by mapping the
clicked image points from one view to the other, and displaying them on top of each respective
image. Be sure to handle homogenous and
non-homogenous coordinates correctly.

# 3 Warping between image planes
Write a function that can take the recovered homography matrix and an image, and return a
new image that is the warp of the input image using H . Since the transformed coordinates
will typically be sub-pixel values, you will need to sample the pixel values from nearby pixels.
For color images, warp each RGB channel separately and then stack together to form the output.
To avoid holes in the output, use an inverse warp. Warp the points from the source image
into the reference frame of the destination, and compute the bounding box in that new reference
frame. Then sample all points in that destination bounding box from the proper coordinates
in the source image (linear interpolation). Note that transforming all the points will generate
an image of a different shape / dimensions than the original input.

# 4 Create the output mosaic
Once we have the source image warped into the destination images frame of reference, we can
create a merged image showing the mosaic. Create a new image large enough to hold both
(registered) views; overlay one view onto the other, simply leaving it black wherever no data is
available. Do not worry about artifacts that result at the boundaries.

# 5 Bonus
1)Replace the manual correspondence stage with automatic interest point detection and
local feature matching.

2)Implement RANSAC for robustly estimating the homography matrix from noisy correspondences.
Show with an example where it successfully gives good results even when
there are outlier (bad) correspondences given as input.
