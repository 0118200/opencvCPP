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
        cerr << "Kamera tidak dapat terbuka!" << endl;
        return -1;
    }

    CascadeClassifier faceCascade;
    if (!faceCascade.load("c:/opencv/sources/data/haarcascades/haarcascade_frontalface_alt2.xml"))
    {
        cerr << "Gagal load model haarcascade!" << endl;
        return -1;
    }

    Mat frame, gray, flipped, equalized;
    vector<Rect> faces;

    while (true)
    {
        cam >> frame;
        if (frame.empty()) break;

        flip(frame, flipped, 1); 
        cvtColor(flipped, gray, COLOR_BGR2GRAY);
        equalizeHist(gray, equalized);

        
        faceCascade.detectMultiScale(equalized, faces, 1.1, 5, 0, Size(100, 100));

        
        for (const Rect &face : faces)
        {
            rectangle(flipped, face, Scalar(0, 255, 0), 2);
        }

        imshow("Face Detection", flipped);

        if (waitKey(10) == 27) break; 
    }

    cam.release();
    destroyAllWindows();
    return 0;
}

```
