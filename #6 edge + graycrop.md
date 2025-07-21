```
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main ()
{
    Mat ASLI = imread("C:/Users/ADVAN/Downloads/kuceng.jpg");
    Mat graycrop;
    Mat edge;

    Rect potong (50,50, 100,100);
    Mat crop = ASLI(potong);
    
    cvtColor (crop, graycrop, COLOR_BGR2GRAY);
    Canny (graycrop, edge, 50,150);

    putText(edge, "Ini edge crop", Point(10,30), FONT_HERSHEY_SIMPLEX, 0.4, Scalar(255), 1);

    imshow("EDGE", edge);
    imshow("GRAY", graycrop);
    imshow("CROP", crop);
    imshow("ASLI", ASLI);

    imwrite("C:/Users/ADVAN/Downloads/kucengedge.jpg", edge);
    imwrite("C:/Users/ADVAN/Downloads/kucenggray.jpg", graycrop);
    imwrite("C:/Users/ADVAN/Downloads/kucengcrop.jpg", crop);
    
    waitKey(0);
    return 0;
}
```
