# CNV-BNN_CLASSIFIER

HARDWARE ACCELERATION IN FPGA:

FPGAs are field programmable gate arrays:

As the name suggests, these can be reconfigured and programmed according to the application. Due to their parallel processing capabilities, they are efficient than traditional GPUs.They also have low power consumption

Hardware used: Pynq z2 board

Process:
VITIS 

1.The code is written in C++ in Vitis - it is synthesized
2.Rtl export
3.Export IP : which is a reusable ip which is used in the fpga

VIVADO:

1.Create bLock design
2.Add processor cores and IP cores
3.run automated connections
4.create hdl wrapper
5.generate bitstream file
6.transfer files to pynq board
7.Connect to python api : 
by importing overlay library.
To connect your PYNQ board to your computer, use an Ethernet cable and configure your computer's network settings, either with a static IP address or DHCP. Find the PYNQ board's IP address, accessible through the PYNQ dashboard or by checking your router's connected devices, and enter it in a web browser to access the PYNQ dashboard for further interaction and configuration.

The weights are not trained within this notebook but are pre-trained and loaded onto the Pynq device during the instantiation of the classifier. The dataset is already integrated into the BNN library, and the relevant weights are automatically downloaded based on the specified network configuration and dataset.


1. <b>Importing BNN Library and Initializing Classifier:</b>
   - You start by importing the bnn library, which is designed for working with Binarized Neural Networks.
   - You initialize a hardware classifier (classifier) using the CnvClassifier class from the bnn library. This classifier is set to run on FPGA (bnn.RUNTIME_HW).

2.Load and Display Images:Loop through a directory of images, open each image, resize it to 64x64 pixels, and display it using IPython's display function

3.Hardware-based Classification:

results = classifier.classify_images(images): Use the hardware-accelerated classifier to identify classes for the loaded images.


Initialize a software-based BNN classifier for the same network.:

sw_class = bnn.CnvClassifier(bnn.NETWORK_CNVW1A1,"road-signs", bnn.RUNTIME_SW): I
results = sw_class.classify_images(images):
Loop through the results and print the corresponding class names.

4.Object Detection on a Single Image:

Load an image file (street_with_stop.JPG) and crop it into smaller tiles.
results = classifier.classify_images(images): Use the hardware-accelerated classifier to identify classes for the cropped tiles.
Identify the indices corresponding to the "stop" sign class (assuming class 14).
Draw rectangles around the identified "stop" signs on the original image

5.Memory management: reset the pynq board

Inference took 145901.00 microseconds, 109.70 usec per image
Classification rate: 9115.77 images per second

Inference took 1252522.97 microseconds, 417507.66 usec per image
Classification rate: 2.40 images per second
Identified classes: [41 27 14]
Identified class name: End of no-overtaking zone
Identified class name: Pedestrians in road ahead
Identified class name: Stop
