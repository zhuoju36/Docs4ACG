# 由曲线网生成蒙皮网格

在空间结构的计算中往往需要生成蒙皮网格，如用于荷载传导的蒙皮，或者空间梁板结构中的板等

ACG提供的几种快速的方法进行相关计算

此处以下图单层网壳模型为例说明，图中的曲线网络，已经打断为离散的线段。

![skin](/_static/img/examples/genskin/1.jpg)

初始化模型，使得功能可用后，通过计算-蒙皮计算进入面板

![skin](/_static/img/examples/genskin/2.jpg)

## 计算生成网格顶点的Delaunay三角蒙皮网格

通过下图入口执行计算

![skin](/_static/img/examples/genskin/3.jpg)

输入误差后可以生成相关网格，如下图所示。Delaunay网格将最大化最小角，但不保证边与给定线段重合

![skin](/_static/img/examples/genskin/4.jpg)

多余网格面可以通过Rhino命令DeleteFace删除，如存在大量狭长的网格面，也可以先通过ExtractMeshFacesByAspectRatio抽离后删除，网格边与线段不重合之处可以通过SwapMeshEdge反转对齐

Delaunay网格在顶点集合的最小二乘平面上投影平面上计算，如曲面卷曲明显，可分片实施

## 计算约束边缘的Delaunay三角蒙皮网格

若线段网络质量较好，可以勾选约束边缘选项，获得更高质量的三角网格，网格将保证边与给定的线段重合，不需要反转边缘，并自动计算排除外围周多余的网格面

![skin](/_static/img/examples/genskin/5.jpg)

## 计算边缘围合的蒙皮网格

生成蒙皮网格的另一种方法是搜索网络中的环，要求给出边数。计算时间随搜索深度增长，为避免花费过高时间和内存导致卡死，不建议输入太高的边数，也可以通过分批计算提高速度

![skin](/_static/img/examples/genskin/6.jpg)

下图给定边数为4，故根据边生成了四边形的网格，而3边的三角网格面没有被生成，如需生成可以输入边数=3再次计算。

![skin](/_static/img/examples/genskin/7.jpg)

如有破洞或其他不能按预期边数生成网格的情况，请检查附近线段是否没有正确连接。










