# Video_compression_using_Singular_Value_Decomposition

Singular Value Decomposition(SVD) is a very strong tool. Every matrix can be decomposed into three different matrices comprising. Suppose we have a matrix A then A=U S V. Now if we have a video of 30 seconds and we decompose it into frames of 30 fps. So total we have 900 frames. 
A class named "SVD_comp" is created. The members are as below
# Member functions and Working of each: 
i) constructors: Takes path---> path where video shall be stored , 
  image_cap_path----> path to store the image frames, 
  imr---> red layer storing path,
  imb---> blue layer storing path,
  img---> green layer storing path,
  vnm---> Name to be given to the reconstructed video,
  n_components---> Number of components to be considered i.e. number of singular values to be considered,
  storage_path---> the path where the final video to be stored,
  partition parameters----> This is check or flag variable. If the images are already converted to frames then the value is set to False. But if original video is provided and the   frame dissociation is not done, then set it to True.
To preserve abstraction, our constructor will call the subsequent functions.
ii) partition_video()---> This function does not accept any parameter and is actually designed to convert the video into frames by sampling at 30 frames per second. It actually can create an extra frame which is actually blank. So it is deleted. 
iii) capturing_image_data() ----> This is a non-parameterized function. In this function, we actually read all the frames one by one. Resize it into 100 x 100 images.(As higher dimensions require more processing power). Now we read the images from the path where the frames were stored. Now after reading the images, it is dissociated into Red , Blue and Green layer matrices. imgr---> gives red layer matrix value, imgg---> gives green layer matrix value, imgb---> gives blue layer matrix value.
iv) svd_compression()--> Takes 2 parameter image_vec_mat i.e. the image vector matrix and the name of the channel it is considering i.e. Red, Green Blue (RGB). After that we have obtained the image matrices for all three layers, we reshape it appropriately and then apply Singular Value Decomposition on it. If suppose M is my original matrix. svd(M) returns 3 matrices U S V. U and V are 2 unitary matrices where U= eigen vector matrix(transpose(M) * M) and V = eigen vector matrix( M * transpose(M) ). S= diagonal matrix. Now we extract the maximum n components from S array which will signify my most important components in the matrix that produces the maximum information. Now those values that are already selected are converted into a very high negative value, here -1000 so that they are not repeated again and again.

After doing these, we find the final compression of the video frames. Also we display the amount of error that took place after reconstruction. 
Error = || original_image - reconstructed_image ||... where ||x|| is actually the frobenius norm of the difference.
Hence, we finally display the amount of compression that actualy took place in the process. After this, we down sample the reconstructed_image to 480 x 270. This might cause blurring of image but 100 x 100 will surely lead bursting of image pixels when converted into video file.
Repeat this process for all 3 layers. Finally store these layer images in respective files mentioned during initialisation.
Now combine all the 3 layers so that we get back RGB files. Finally using Computer vision(cv2) we write the images continuously in form of a video file.
