# 96Neko-Xzqh-ChinaShapefiles
> 96Neko Projects : China Shapefiles for Data Analysis
>
> 用于数据分析的中国地理数据shapefile文件



## 介绍

shapefile格式的地理数据文件。以行政区划层级划分为4组，每组8个文件，所含数据为行政区域的多边形表示，文件元数据中包含每个行政区域的代码与名称，所含属性与含义见后文介绍

- `China_Full`：Level 0，全国完整区域数据，无划分

- `China_ProvinceLevel`：Level 1，一级行政区（省、直辖市、自治区、特别行政区）边界划分的区域数据

- `China_PrefectureLevel`：Level 2，二级行政区（地级市、地区、自治州、盟等）边界划分的区域数据

行政区域数据与行政区划代码数据截至**2019年12月**



## 预览方法

shapefile可使用ArcGIS套件查看与编辑，亦可使用Python进行预览操作

> requirements：`pyproj`、`Basemap`
>
> **（Windows平台下）以上两依赖项建议转至[此链接处](https://www.lfd.uci.edu/~gohlke/pythonlibs/)下载预编译的whl文件进行安装**
>
> 1. 导入需要的包
>
>    ```python
>    import matplotlib.pyplot as plt
>    from mpl_toolkits.basemap import Basemap
>    ```
>
> 2. 初始化Basemap对象
>
>    **设置地图的范围为正好显示中国全境，投影方式为墨卡托投影，绘制精度为高
>
>    ```python
>    map = Basemap(
>    	llcrnrlon = 72,		# lower left corner longitude == 地图左下角顶点经度
>        urcrnrlon = 137,	# upper right corner longitude == 地图右上角顶点经度
>        llcrnrlat = 2,		# lower left corner latitude == 地图左下角顶点纬度
>        urcrnrlat = 55,		# upper right corner latitude == 地图右上角顶点纬度
>        projection = 'merc', # 投影方式
>        resolution = 'h'	# 分辨率，可选值可参考Basemap官方文档
>    )
>    ```
>
> 3. 载入shapefile并显示
>
>    ```python
>    map.readshapefile(
>    	'%path of shapefile%',	# 此处给出想要预览的shapefile路径，不要包含任何文件扩展名
>        '%name for manage%',	# 管理元数据时用到的标签名称，预览时可不给出
>        drawbounds = True
>    )
>    plt.show()
>    ```



## 其他

**注1：Level 2中的一些约定**

* **北京市、天津市、上海市、重庆市**分别作为单一区域，其中**重庆市**不区分所辖区县
* **海南省**所辖地级行政区与县级行政区同等对待，分别作为单一区域
* **新疆维吾尔自治区**直辖的师市合一县级行政区暂缺边界数据，除石河子市以外与原所属的二级行政区作为单一区域
* **台湾省**按照现状行政区域划分，市县同等对待，分别作为单一区域