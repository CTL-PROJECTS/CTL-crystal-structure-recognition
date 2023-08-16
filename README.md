General information about the CTL course available at https://ctl.polyphys.mat.ethz.ch/

# :wave: PROJECT crystal-structure-recognition

Starting from self-generated 'training' set of N different images, each showing one out of P different (defect-free) crystal lattices from different viewpoints, this module returns the best estimate for the crystal structure shown on a newly provided 'test' image, that may not be contained in the training set. The module can also be called with more than a one test image, a set of test images, and then returns the set of recognized crystal structures. All images passed over to this module have an identical number of pixels, px pixels in vertical and py pixels in horizontal direction, and must not show exactly the same portions of the crystals. The (color or grayscale) value of each pixel must be encoded by an integer number between 0 (black) and 255 (white).
The goal is to correctly and quickly identify crystal lattices from single and multiple test images. This module may make use of existing libraries such as tensorflow (python) or fitensemble (matlab). 

The structure of your final code could be as follows:

    ...
    
    def create_training_data(N)
    ...
    
    def load_training_data():
        ...
        return px,py,N,X,y


    create_training_data(50)
    px,py,N,X,y = load_training_data()
    
    if len(sys.argv)-1==1:
        y_result = crystal_recognition(str(sys.argv[1]))
    else:
        y_selected = create_test_data(5)
        y_result = crystal_recognition('lattices-X-test.dat')
        # task 5: compare y_selected with y_result 
    
## Task 1: create_training_data(N)

Here you create N snapshots (px $\times$ py grey-scale pixel images) for each of the at least four different 3D lattices (named 1,2,3,4), and save all images into lattices-X-train.dat (single line per image, to this end unfold a 2D array of pixel values into a one-dimensional array; each line of lattices-X-train.dat contains px $\times$ py integer values $\in$ {0,1,..,255}). Save the corresponding lattice numbers in lattices-y-train.dat (both files then have the same number of rows). Save your chosen value for px (and py) in files lattices-pixelX.dat and lattices-pixelY.dat.

This function hence creates the following four files
1. lattices-pixelX.dat
2. lattices-pixelY.dat 
3. lattices-X-train.dat
4. lattices-y-train.dat

The first two contain information about the number of pixels of the images saved in the third file (each image is encoded by pixel intensities, stored in a single line with px $\times$ py integer values), and the fourth file contains the names (integer values) of lattices belonging to the images. 

## Task 2: load_training_data()

Create a function load_training_data() that does the following:

1. read the single integer px from lattices-pixelX.dat
2. read the single integer py from lattices-pixelY.dat
3. read all rows from lattices-X-train.dat. Each row has px $\times$ py columns (the pixel intensities of the image). Denote this field by X.
4. read all rows from lattices-y-train.dat. Each row carries a single integer (the crystal type). Denote this field by y.
5. Return px,py,N,X,y

## Task 3: visualize_data(n)

Create a function that 

1. loads the training data
2. visualizes the image (px x py pixels) contained in the nth row of X

## Task 4: create_test_data(T)

This function

1. loads the training data
2. randomly selects T < N rows
3. Writes the selected rows of X into a file lattices-X-test.dat
4. Returns the selected rows of y (call it y_selected)

## Task 5: crystal_recognition(Xtestfile)

This function

1. reads the content of the file lattices-X-test.dat (call it Xtest) and determines its number of rows (T).
2. for each of the T rows of Xtest, suggests a name of the lattice shown, and saves the names (integer array denoted as y_result) in a file lattices-y-test.dat. This latter file should have T rows and a single column. 
3. returns y_result

## Task 6: self test

Calculate and report the difference between y_selected and y_result and the success %. The success % is defined by the fraction of successfully recognized crystal lattices. This self test is only possible if the test data was generated using the training data. We will test your code using test data that is not contained in the training data. 

## Task 7: explore the success % of the recognition software

1. Add random numbers to the coordinates of the ideal lattices
2. Add defects
      
## Hints

If you wish to use [tensorflow](https://www.tensorflow.org/) to solve this problem, note that tensorflow vs2 or higher may be required to run in python 3.8 or higher. To still use tensorflow compatible with python 3.7, say, you can create a new conda environment for python 3.7 and use it in vscode as described [in the conda section of our CTL-README.md](https://github.com/mkmat/ETH-Computational-Thinking-Labs/blob/main/README.md#conda). 

## Further reading

[using CrystalFeatures to predict the bandgap](https://colab.research.google.com/drive/16WPzzd9nVshAw8ecSPqzGUNiASt7ojvg?usp=sharing#scrollTo=ldW1ubnuf41N)
