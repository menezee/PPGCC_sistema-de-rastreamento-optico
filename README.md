# PPGCC_sistema-de-rastreamento-optico

VideoTracking.java recognizes and tracks every white circle with R > 250 and more than 13 pixels of size

UI built with WindowBuilder https://eclipse.org/windowbuilder
lib used http://opencv.org

For the purpose of this project, 3 algorithms were implemented:

	Tracking by nearest point
	Tracking by image comparison
	Tracking based on model

Methods:

	void findCircles(Mat mat) find every circle containing a pixel with intensity > 250
	void floodFillCircle(Position seed, Mat m, HashMap<String, Position> positions) called recursively in order to find every seed's neighboor with intensity > 100 and include it in positions, where are stored all white pixels of the marker

	void clear() clears temp data structures

	@Deprecated
	void findConnectionsInCirclesFound() create skeleton connection for nearest marker without previous connection

	int getIntensity(double[] BGR) calcs BGR[1] * 0.587 + BGR[2] * 0.299 + BGR[0] * 0.114

	void initUIComponents() initialize windowbuilder panels

	updateImage(Mat m, JLabel label, String frame) saves frame image with frame number as title and sets it on window label containing the image displayed

	int[][] findMatrixAroundCircle(Circle c, Mat m) returns binary matrix 15x15 around c in m

	void printMatrix(int[][] matrix) prints matrix on console

	int calculateSumOfAbsoluteDifferencesBetween(int[][] m1, int[][] m2) calculates the sum of absolute difference comparing m1 and m2

void main(String[] args)
features within main not declared outside:
calculates the center for every marker found
tracks the markers and draw the skeleton lines
calls different algorithms based on static int ALGORITHM

temp data structures:

	static List<HashMap<String, Position>> circles stores every circle only with its pixels (key: x+y, value: class Position stores x and y - equivalent to opencv Point)
	static HashMap<String, Position> visitedWhitePixels contains all visited white pixels to check before flooding new marker
	static List<Circle> circlesDiscovered actual circle class


Classes needed:

	Cirle
	private HashMap<String, Position> pixels;
	private int id;
	private Position position;
	private Circle connectsTo;
	private int connectionDistance;
	private int[][] matrix;
	private Scalar color;

	Position
	int y, x;

	Frame
	private int id;
	private Mat mat;
	private List<Circle> circles;

Demonstration:
https://www.youtube.com/watch?v=gAnwEJ-dWTk