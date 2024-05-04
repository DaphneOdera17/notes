# OpenCV | 项目 | 虚拟绘画
## 捕捉摄像头
如果在虚拟机中运行，请确保虚拟机摄像头打开。
```cpp
#include<opencv2/opencv.hpp>

using namespace cv;
using namespace std;

int main()
{
    VideoCapture cap(0);

    Mat img;
    
    while(1) {
        cap.read(img);
        imshow("Image", img);
        waitKey(1);
    }

    return 0;
}
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503135302.png)
### 捕捉对应单一颜色
myColors 的颜色值对应 hmin smin vmin hmax smax vmax
```cpp
#include<opencv2/opencv.hpp>

using namespace cv;
using namespace std;

vector<vector<int>> myColors {{109,125,66,179,209,215}, // red
                              {35, 81, 131, 52, 255, 214}}; // Green

vector<Scalar> myColorValues{   {0, 0, 255}, // red
                                {0, 255, 0}}; // Green

Mat img;

void findColor(Mat img)
{
    Mat imgHSV;
    cvtColor(img, imgHSV, COLOR_BGR2HSV);
    
    for(int i = 0; i < myColors.size(); i ++)
    {
        Scalar lower(myColors[i][0], myColors[i][1], myColors[i][2]);
        Scalar upper(myColors[i][3], myColors[i][4], myColors[i][5]);

        Mat mask;
        inRange(imgHSV, lower, upper, mask);

        imshow(to_string(i), mask);
    }
}

int main()
{
    VideoCapture cap(0);
    
    while(1) {
        cap.read(img);

        findColor(img);

        imshow("Image", img);
        waitKey(1);
    }

    return 0;
}
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/26ca412c7fcd326aeed2efdbef8adad.png)
### 添加描绘轮廓
```cpp
void getContours(Mat imgDil)
{
    vector<vector<Point>> contours;
    vector<Vec4i> hierarchy;

    findContours(imgDil, contours, hierarchy, RETR_EXTERNAL, CHAIN_APPROX_SIMPLE);

	vector<vector<Point>> conPoly(contours.size());
	vector<Rect> boundRect(contours.size());
    for(int i = 0; i < contours.size(); i ++)
    {
        int area = contourArea(contours[i]);
        cout << area << endl;

        string objectType;

        if(area > 1000) 
        {
            float peri = arcLength(contours[i], true);

            approxPolyDP(contours[i], conPoly[i], 0.02 * peri, true);

            drawContours(img, conPoly, i, Scalar(255, 0, 255), 2);

            cout << conPoly[i].size() << endl;

            boundRect[i] = boundingRect(conPoly[i]);
        }
    }
}

void findColor(Mat img)
{
    Mat imgHSV;
    cvtColor(img, imgHSV, COLOR_BGR2HSV);
    
    for(int i = 0; i < myColors.size(); i ++)
    {
        Scalar lower(myColors[i][0], myColors[i][1], myColors[i][2]);
        Scalar upper(myColors[i][3], myColors[i][4], myColors[i][5]);

        Mat mask;
        inRange(imgHSV, lower, upper, mask);

        imshow(to_string(i), mask);
        getContours(mask);
    }
}
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503144628.png)
![883b27456b42a44fe730c8484118ee4.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/883b27456b42a44fe730c8484118ee4.png)
(不过识别的还是有点抽象的, (逃~))
### 添加边界框
```cpp
void getContours(Mat imgDil)
{
    ...

    for(int i = 0; i < contours.size(); i ++)
    {
        ...
        
        if(area > 1000) 
        {
            ...
            drawContours(img, conPoly, i, Scalar(255, 0, 255), 2);
            rectangle(img, boundRect[i].tl(), boundRect[i].br(), Scalar(0, 255, 0), 5);
        }
    }
}
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503145923.png)
### 绘制
```cpp
#include<opencv2/opencv.hpp>

using namespace cv;
using namespace std;

Mat srcimg;
Mat img;

vector<vector<int>> newPoints;

vector<vector<int>> myColors {{118, 0, 171, 130, 255, 232}, // White
                              {35, 81, 131, 52, 255, 214}}; // Green

vector<Scalar> myColorValues{   {255, 0, 255}, // Purple
                                {0, 255, 0}}; // Green

Point getContours(Mat imgDil)
{
    vector<vector<Point>> contours;
    vector<Vec4i> hierarchy;

    findContours(imgDil, contours, hierarchy, RETR_EXTERNAL, CHAIN_APPROX_SIMPLE);

    vector<vector<Point>> conPoly(contours.size());
    vector<Rect> boundRect(contours.size());

    Point myPoint(0, 0);

    for(int i = 0; i < contours.size(); i ++)
    {
        int area = contourArea(contours[i]);
        cout << area << endl;
        
        string objectType;

        if(area > 1000) 
        {
            float peri = arcLength(contours[i], true);

            approxPolyDP(contours[i], conPoly[i], 0.02 * peri, true);

            cout << conPoly[i].size() << endl;

            boundRect[i] = boundingRect(conPoly[i]);
            myPoint.x = boundRect[i].x + boundRect[i].width / 2;
            myPoint.y = boundRect[i].y;

            drawContours(img, conPoly, i, Scalar(255, 0, 255), 2);
            rectangle(img, boundRect[i].tl(), boundRect[i].br(), Scalar(0, 255, 0), 5);
        }
    }

    return myPoint;
}

vector<vector<int>> findColor(Mat img)
{
    Mat imgHSV;
    cvtColor(img, imgHSV, COLOR_BGR2HSV);
    
    for(int i = 0; i < myColors.size(); i ++)
    {
        Scalar lower(myColors[i][0], myColors[i][1], myColors[i][2]);
        Scalar upper(myColors[i][3], myColors[i][4], myColors[i][5]);

        Mat mask;
        inRange(imgHSV, lower, upper, mask);

        imshow(to_string(i), mask);
        Point myPoint = getContours(mask);

        if(myPoint.x != 0 && myPoint.y != 0)
            newPoints.push_back({myPoint.x, myPoint.y, i});
    }
    return newPoints;
}

void drawOnCanvas(vector<vector<int>> newPoints, vector<Scalar> myColorValues)
{
    for(int i = 0; i < newPoints.size(); i ++)
    {
        circle(img, Point(newPoints[i][0], newPoints[i][1]), 10, myColorValues[newPoints[i][2]], FILLED);
    }
}


int main()
{
    VideoCapture cap(0);
    
    while(1) {
        cap.read(srcimg);
        Mat resultImage2;
	    flip(srcimg, img, 1);

        newPoints = findColor(img);
        drawOnCanvas(newPoints, myColorValues);

        imshow("Image", img);
        waitKey(1);
    }

    return 0;
}
```
可以根据捕获到的物体来进行绘制（我这里代码采用了白色物体，取值不是很准确，所以会有断断续续的点。）
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503160836.png)
