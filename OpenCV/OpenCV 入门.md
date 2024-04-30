# OpenCV | 入门
## 安装
[参考教程](https://www.samontab.com/web/2023/02/installing-opencv-4-7-0-in-ubuntu-22-04-lts/)
## 基础知识
$VGA = 640 \times 480$
$HD = 1280 \times 720$
$FHD = 1920 \times 1080$
$4K = 3840 \times 2160$
这些都表示了固定的像素，例如 VGA，代表在宽度上 640 像素(px)，在高度上 480 像素。我们可以把这些像素看成一个一个框。
对于黑白图像 Binary Image, 用 0 代表黑色，用 1 代表白色。

对于 8 位，可以表示 $2^8 = 256$ 个级别，也就是 0 ~ 255。一个灰度图像(Gray Scale Image) 也就是 8 Bit or 256 Level 的。
## 显示图像
图片与代码放在同个目录下。
```cpp
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <opencv2/imgproc.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main()
{
    /* Importing Images */
    string path = "../dog.jpeg";
    Mat img = imread(path);

    imshow("Image", img);
    waitKey(0);
}
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240429234108.png)
## 将图片转换为灰度图像
```cpp
string path = "../dog.jpeg";
Mat img = imread(path);
Mat imgGray;

/* 转换图像颜色 */
cvtColor(img, imgGray, COLOR_BGR2GRAY);

imshow("Image", img);
imshow("Image Gray", imgGray);
waitKey(0);
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240429234218.png)
