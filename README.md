# imu_utils

A ROS package tool to analyze the IMU performance. C++ version of Allan Variance Tool. 
The figures are drawn by Matlab, in `scripts`.

Actually, just analyze the Allan Variance for the IMU data. Collect the data while the IMU is Stationary, with a two hours duration.

## refrence

Refrence technical report: [`Allan Variance: Noise Analysis for Gyroscopes`](http://cache.freescale.com/files/sensors/doc/app_note/AN5087.pdf "Allan Variance: Noise Analysis for Gyroscopes"), [`vectornav gyroscope`](https://www.vectornav.com/support/library/gyroscope "vectornav gyroscope") and 
[`An introduction to inertial navigation`](http://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-696.html "An introduction to inertial navigation").

```
Woodman, O.J., 2007. An introduction to inertial navigation (No. UCAM-CL-TR-696). University of Cambridge, Computer Laboratory.
```
Refrence Matlab code: [`GyroAllan`](https://github.com/XinLiGitHub/GyroAllan "GyroAllan")

## IMU Noise Values

Parameter | YAML element | Symbol | Units
--- | --- | --- | ---
Gyroscope "white noise" | `gyr_n` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_g}"> | <img src="https://latex.codecogs.com/svg.latex?{%5Cfrac%7Brad%7D%7Bs%7D%5Cfrac%7B1%7D%7B%5Csqrt%7BHz%7D%7D}">
Accelerometer "white noise" | `acc_n` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_a}"> | <img src="https://latex.codecogs.com/svg.latex?{%5Cfrac%7Bm%7D%7Bs^2%7D%5Cfrac%7B1%7D%7B%5Csqrt%7BHz%7D%7D}">
Gyroscope "bias Instability" | `gyr_w` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_b_g}"> | <img src="http://latex.codecogs.com/svg.latex?\frac{rad}{s}&space;\sqrt{Hz}" title="\frac{rad}{s} \sqrt{Hz}" />
Accelerometer "bias Instability" | `acc_w` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_b_a}"> | <img src="http://latex.codecogs.com/svg.latex?\frac{m}{s^2}&space;\sqrt{Hz}" title="\frac{m}{s^2} \sqrt{Hz}" />

* White noise is at tau=1;

* Bias Instability is around the minimum;

(according to technical report: [`Allan Variance: Noise Analysis for Gyroscopes`](http://cache.freescale.com/files/sensors/doc/app_note/AN5087.pdf "Allan Variance: Noise Analysis for Gyroscopes"))

## sample test

<img src="figure/gyr.jpg">
<img src="figure/acc.jpg">

* blue  : Vi-Sensor, ADIS16448, `200Hz`
* red   : 3dm-Gx4, `500Hz`
* green : DJI-A3, `400Hz`
* black : DJI-N3, `400Hz`
* circle : xsens-MTI-100, `100Hz`

## How to build and run?

### to build

```
sudo apt-get install libdw-dev
```

* download required [`code_utils`](https://github.com/gaowenliang/code_utils "code_utils");

* 分别build `imu_utils` 和 `code_utils`



### to run

```
source devel/setup.bash
```

* collect the data while the IMU is Stationary, with a two hours duration; (or) play rosbag dataset;

```
rosbag play -r200 ~/rosbag/intrin-imu-calib/intrin-imu-calib.bag 
```

**修改launch文件**

打开imu_utils下面有一堆launch文件，将A3.launch复制并重命名为test.launch,打开，将下面的value换成你自己的IMU数据topic,下面的120是读取数据时间长度，录了俩小时就写120。

![image](https://github.com/countsp/imu_utils/assets/102967883/412375b2-c9c0-4e0d-83d0-6258f7f3988e)

```
roslaunch imu_utils test.launch 
```

### sample output:

```
type: IMU
name: A3
Gyr:
   unit: " rad/s"
   avg-axis:
      gyr_n: 1.0351286977809465e-04
      gyr_w: 2.9438676109223402e-05
   x-axis:
      gyr_n: 1.0312669892959053e-04
      gyr_w: 3.3765827874234673e-05
   y-axis:
      gyr_n: 1.0787155789128671e-04
      gyr_w: 3.1970693666470835e-05
   z-axis:
      gyr_n: 9.9540352513406743e-05
      gyr_w: 2.2579506786964707e-05
Acc:
   unit: " m/s^2"
   avg-axis:
      acc_n: 1.3985049290745563e-03
      acc_w: 6.3249251509920116e-04
   x-axis:
      acc_n: 1.1687799474421937e-03
      acc_w: 5.3044554054317266e-04
   y-axis:
      acc_n: 1.2050535351630543e-03
      acc_w: 6.0281218607825414e-04
   z-axis:
      acc_n: 1.8216813046184213e-03
      acc_w: 7.6421981867617645e-04
```

## dataset

DJI A3: `400Hz`

Download link: [`百度网盘`](https://pan.baidu.com/s/1jJYg8R0 "DJI A3")


DJI A3: `400Hz`

Download link: [`百度网盘`](https://pan.baidu.com/s/1pLXGqx1 "DJI N3")


ADIS16448: `200Hz`
 
Download link:[`百度网盘`](https://pan.baidu.com/s/1dGd0mn3 "ADIS16448")

3dM-GX4: `500Hz`

Download link:[`百度网盘`](https://pan.baidu.com/s/1ggcan9D "GX4")

xsens-MTI-100: `100Hz`

Download link:[`百度网盘`](https://pan.baidu.com/s/1i64xkgP "MTI-100")


# 标定结果
```
office2004@office2004-HP-Z2-Tower-G9-Workstation-Desktop-PC:~/catkin_ws/imu_utils-master$ roslaunch imu_utils test.launch 
... logging to /home/office2004/.ros/log/963bb0c8-3a8e-11ef-9797-2b170f60219f/roslaunch-office2004-HP-Z2-Tower-G9-Workstation-Desktop-PC-1063075.log
Checking log directory for disk usage. This may take a while.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.

started roslaunch server http://office2004-HP-Z2-Tower-G9-Workstation-Desktop-PC:46701/

SUMMARY
========

PARAMETERS
 * /imu_an/data_save_path: /home/office2004/...
 * /imu_an/imu_name: A3
 * /imu_an/imu_topic: /imu_data
 * /imu_an/max_cluster: 100
 * /imu_an/max_time_min: 116
 * /rosdistro: noetic
 * /rosversion: 1.16.0

NODES
  /
    imu_an (imu_utils/imu_an)

ROS_MASTER_URI=http://localhost:11311

process[imu_an-1]: started with pid [1063112]
[ INFO] [1720159424.853752516]: Loaded imu_topic: /imu_data
[ INFO] [1720159424.854358004]: Loaded imu_name: A3
[ INFO] [1720159424.854536981]: Loaded data_save_path: /home/office2004/catkin_ws/imu_utils-master/src/data/
[ INFO] [1720159424.854704841]: Loaded max_time_min: 116
[ INFO] [1720159424.854861258]: Loaded max_cluster: 100
gyr x  num of Cluster 100
gyr y  num of Cluster 100
gyr z  num of Cluster 100
acc x  num of Cluster 100
acc y  num of Cluster 100
acc z  num of Cluster 100
wait for imu data.
gyr x  numData 696405
gyr x  start_t 1.67889e+09
gyr x  end_t 1.6789e+09
gyr x dt 
-------------6961.29 s
-------------116.021 min
-------------1.93369 h
gyr x  freq 100.04
gyr x  period 0.00999605
gyr y  numData 696405
gyr y  start_t 1.67889e+09
gyr y  end_t 1.6789e+09
gyr y dt 
-------------6961.29 s
-------------116.021 min
-------------1.93369 h
gyr y  freq 100.04
gyr y  period 0.00999605
gyr z  numData 696405
gyr z  start_t 1.67889e+09
gyr z  end_t 1.6789e+09
gyr z dt 
-------------6961.29 s
-------------116.021 min
-------------1.93369 h
gyr z  freq 100.04
gyr z  period 0.00999605
Gyro X 
C  -3.42739   292.523  -47.7044   20.1352 -0.286042
 Bias Instability 0.000467813 rad/s
 Bias Instability 0.000475073 rad/s, at 24.7402 s
 White Noise 45.2518 rad/s
 White Noise 0.0129637 rad/s
  bias 0.425267 degree/s
-------------------
Gyro y 
C  -3.66663   288.267  -44.1722   24.8118 -0.213034
 Bias Instability 0.00039165 rad/s
 Bias Instability 0.000548127 rad/s, at 13.1748 s
 White Noise 45.5857 rad/s
 White Noise 0.0129621 rad/s
  bias 1.05489 degree/s
-------------------
Gyro z 
C  -2.43692    336.17  -19.1008   10.9322 -0.184417
 Bias Instability 0.000445787 rad/s
 Bias Instability 0.000413134 rad/s, at 59.7664 s
 White Noise 56.8144 rad/s
 White Noise 0.0160658 rad/s
  bias -0.403409 degree/s
-------------------
==============================================
==============================================
acc x  numData 696405
acc x  start_t 1.67889e+09
acc x  end_t 1.6789e+09
acc x dt 
-------------6961.29 s
-------------116.021 min
-------------1.93369 h
acc x  freq 100.04
acc x  period 0.00999605
acc y  numData 696405
acc y  start_t 1.67889e+09
acc y  end_t 1.6789e+09
acc y dt 
-------------6961.29 s
-------------116.021 min
-------------1.93369 h
acc y  freq 100.04
acc y  period 0.00999605
acc z  numData 696405
acc z  start_t 1.67889e+09
acc z  end_t 1.6789e+09
acc z dt 
-------------6961.29 s
-------------116.021 min
-------------1.93369 h
acc z  freq 100.04
acc z  period 0.00999605
acc X 
C -9.61565e-06  0.000618178 -8.47061e-05  2.03329e-05  2.40374e-07
 Bias Instability 0.000142058 m/s^2
 White Noise 0.00560175 m/s^2
-------------------
acc y 
C -6.12689e-06  0.000630708 -5.27174e-05  1.81475e-05  2.25265e-07
 Bias Instability 0.000157498 m/s^2
 White Noise 0.00596762 m/s^2
-------------------
acc z 
C -6.38149e-05   0.00104845 -0.000297417   3.6852e-05  -5.8536e-07
 Bias Instability 0.000155338 m/s^2
 White Noise 0.00632892 m/s^2
-------------------
[imu_an-1] process has finished cleanly
log file: /home/office2004/.ros/log/963bb0c8-3a8e-11ef-9797-2b170f60219f/imu_an-1*.log
all processes on machine have died, roslaunch will exit
shutting down processing monitor...
... shutting down processing monitor complete
done
```
