```
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main()
{
    VideoCapture cam(0);
    if (!cam.isOpened())
    {
        cerr << "Kamera tidak terbuka" << endl;
        return -1;
    }

    Mat frame, flipped;
    while (true)
    {
        cam >> frame ;
        if (frame.empty()) break;

        flip(frame, flipped, 1);

        imshow ("Webcam", flipped);

        if (waitKey(1) == 'q' ) break;
    }

    cam.release();
    destroyAllWindows();
    return 0;
}
```
