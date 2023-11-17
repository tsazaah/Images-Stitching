# Images-Stitching

## Daftar Isi
- [Install Packages yang Akan Digunakan](#Install-Packages-yang-Akan-Digunakan)
- [Eksekusi Images Stitching](Eksekusi-Images-Stitching)
  
## Install Packages yang Akan Digunakan

1. Menginstall Imutils
   Untuk mengintall library tersebut gunakan perintah
   ```bash
   pip3 install imutils
   ```
2. Menginstall opencv
   Untuk mengistallnya gunakan peritah
   ```bash
   Pip3 install opencv-python
   ```
4. Menginstall mathplotlib
   ```bash
   Pip3 install mathplotlib
   ```

## Eksekusi Images Stitching
1. Masuk ke dalam direktori yang berisi kodingan image stitching dan didalamnya terdapat direktori image  yang akan digabungkan
   
   ![image](https://github.com/tsazaah/Images-Stitching/assets/150001965/698326c8-f595-4626-bba1-09161ef10ca9)
   image_stitching_simple.py merupakan program yang akan digunakan untuk mengeksekusi image stitching. 
   Direktori images yang akan digabungkan:
   
   ![image](https://github.com/tsazaah/Images-Stitching/assets/150001965/2f93ed05-509d-479c-91b1-9c5978155fc8)
3.	image_stitching_simple.pyberisi kodingan sebagai berikut.
   ```bash
   # USAGE
# python image_stitching_simple.py --images images/scottsdale --output output.png

# import the necessary packages
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", type=str, required=True,
	help="path to input directory of images to stitch")
ap.add_argument("-o", "--output", type=str, required=True,
	help="path to the output image")
args = vars(ap.parse_args())

# grab the paths to the input images and initialize our images list
print("[INFO] loading images...")
imagePaths = sorted(list(paths.list_images(args["images"])))
images = []

# loop over the image paths, load each one, and add them to our
# images to stich list
for imagePath in imagePaths:
	image = cv2.imread(imagePath)
	images.append(image)

# initialize OpenCV's image sticher object and then perform the image
# stitching
print("[INFO] stitching images...")
stitcher = cv2.createStitcher() if imutils.is_cv3() else cv2.Stitcher_create()
(status, stitched) = stitcher.stitch(images)

# if the status is '0', then OpenCV successfully performed image
# stitching
if status == 0:
	# write the output stitched image to disk
	cv2.imwrite(args["output"], stitched)

	# display the output stitched image to our screen
	cv2.imshow("Stitched", stitched)
	cv2.waitKey(0)

# otherwise the stitching failed, likely due to not enough keypoints)
# being detected
else:
	print("[INFO] image stitching failed ({})".format(status))
```
4. Kemudian masukan perintah dibawah ini untuk mengeksekusinya
   ```bash
   python3 image_stitching_simple.py --images images/scottsdale --output output.png
   ```
   atau dapat menggunakan perintah
   ```bash
   python image_stitching.py --images images/scottsdale --output output.jpg \
	--crop 1
   ```
6. Kemudian akan muncul output berupa gambar yang telah digabungkan.
  ![image](https://github.com/tsazaah/Images-Stitching/assets/150001965/6bdb76c5-8307-47bc-ade5-8440d14ac826)

  Output:
  
  ![image](https://github.com/tsazaah/Images-Stitching/assets/150001965/0d23b99b-e9b7-4fb3-a05c-0b69901d997e)

