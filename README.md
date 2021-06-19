# Chess Board Recognition

Recognition of a chess board and pieces using image processing techniques such as enhancement, filtering and segmentation. Final project for Digital Image Processing course at USP - São Carlos. Our aim is to process the images and reconstruct the FEN (Forsyth-Edwards Notation) of the current match represented on the board.

## Contributors

- André Fakhoury
- Gustavo Soares

## Main objective

The main objective of this project is to recognise a chess position using a image of a chess board as input, utilising some techniques of Digital Image Processing and a Convolutional Neural Network. The chess position will be represented using the Forsyth-Edwards Notation (FEN).

## Input dataset

The dataset is a mix of already existent photos from [online repositories](github.com/samryan18/chess-dataset) and new ones taken by us, like screenshot from online chess tools (from [chess.com](chess.com) and [lichess.org](lichess.org)) and photos from a physical chess board and pieces. They consist of a upper view of a chess board, and the filenames are the FEN of the current position.

## Description of methods used

The image preprocessing is done using OpenCV and Numpy. Basically, the pipeline done in this project is:

#### 1. Read the image
First of all, the image is read (using the library imageio), and then converted to grayscale.

#### 2. Process image to reduce noise
Now, the image receives some processing: a Gaussian Blur to reduce the noise and a Canny method to detect the edges of the figure. After that, a morphological operation of Dilation is done to fill some gaps on the edges.

Then, we utilise the findContours method from OpenCV to find the coordinates of the image borders. Now, as the chessboard can be seen as a regular polygon, we apply the approxPolyDP to approximate every contour to another closed shape, consisting of a smaller number of vertices.

#### 3. Locate the chessboard
With the contours extracted and minimized to a simpler shape, we can try to locate all the squares of the image - and then, it's expected that the chessboard is a square with a lot of squares inside.

#### 4. Crop the image to fit the board
With the board correctly located, we can use its corners to delimit the image sides. It helps to ignore some extra noise and useless information that may exist outside the board, so the next step can be done easier.

#### 5. Analyse the pieces and their respective positions
In this step, we use a convolutional neural network to analyse the pieces on each cell of the board. It's not done (yet).
