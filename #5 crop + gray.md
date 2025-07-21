```
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace cv;
using namespace std;

int main ()
{
    Mat ASLI = imread("C:/Users/ADVAN/Downloads/dadu.webp");
    if(ASLI.empty())
    {
        cerr << "Gambarnya gaada bang" << endl;
    }
    else
    {
        cout << "Gambarnya ada kang" << endl;
    }
    Rect croptop(100,140,200,200);
    Mat crop = ASLI(croptop);

    imshow("CROP", crop);
    
    Mat gray;
    cvtColor(ASLI, gray, COLOR_BGR2GRAY);
    
    imshow("gray", gray);

    bool success = imwrite("C:/Users/ADVAN/Downloads/dadugray.webp", gray);
    if(!success)
    {
        cerr << "Gambar tidak tersimpan" << endl;
    }
    else 
    {
        cout << "Gambar tersimpan di : C:/Users/ADVAN/Downloads/dadugray.webp " << endl;
    }

    cout << "tipe gray : " << gray.type() << endl ;

    imwrite("C:/Users/ADVAN/Downloads/daducrop.webp", crop);
    waitKey(0);
    return 0;
}
```
