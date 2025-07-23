```
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace cv;
using namespace std;

int main()
{
    VideoCapture cam(0);
    if (!cam.isOpened())
    {
        cerr << "Kamera tidak dapat terbuka !" << endl ;
        return -1;
    }

    Mat frame, flipped;
    while(true)
    {
        cam >> frame;
        if(frame.empty()) break;

        flip (frame, flipped, 1);
        imshow("WEBCAM", flipped);
        
        int roiWidth = 200;
        int roiHeight = 200;

        int x = (flipped.cols - roiWidth) /2;
        int y = (flipped.rows - roiHeight) /2;

        Rect roi (x, y, roiWidth, roiHeight);
        Mat crop = flipped(roi);

        imshow("CROP", crop);

        Mat grey;
        cvtColor(flipped, grey, COLOR_BGR2GRAY);

        imshow("GREY", grey);

        Mat edge;
        Canny(grey, edge, 50, 150);

        imshow("EDGE", edge);

        if(waitKey(1) == 'q') break;
    }

    cam.release();
    destroyAllWindows();
}
```
