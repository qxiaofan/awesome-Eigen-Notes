由微信公众号「3D视觉工坊」博主整理。

这里简单汇总下我对Eigen库的一点学习心得

####  一 Eigen库的配置

Eigen库相对于其他库而言，配置起来较为简单。

在CMakeLists.txt中，我们可以添加一条命令即可：(假设eigen库被我们放在了目录ThirdParty文件夹下)

include_directories(

${PROJECT_SOURCE_DIR}/ThirdParty/eigen3 

)



#### 二 Eigen库的使用

1、Eigen的子矩阵操作(block)

在Eigen中最基本的块操作运算是运用.blockl()完成的，提取的子矩阵分为动态大小和固定大小。

| 块操作                        | 构建动态大小子矩阵      |
| ----------------------------- | ----------------------- |
| 提取块大小为(p,q),起始于(i,j) | `matrix.block(i,j,p,q)` |

```
Eigen::Matrix4d T ;
T<< 0.018254,-0.999833,0,3.92858,
0.999833, 0.018254, 0, 6.17556,
0, 0, 1, 0,
0, 0, 0, 1;
Eigen::Vector3d t = T.block(0,3,3,1);//相当于从起始位置（0,3），提取块大小为3行一列的块
std::cout<<"t == "<<t<<std::endl;

Eigen::Matrix3d r = T.block(0,0,3,3);
std::cout<<"r == "<<r<<std::endl;

Eigen::Vector3d eular_angle =r.eulerAngles(2,1,0); //旋转矩阵转换为欧拉角
double pi = acos(-1);
eular_angle = eular_angle* 180/pi;
std::cout<<"eular_angle == "<<eular_angle<<std::endl;
```

更新于2020年12月23日，持续完善中。