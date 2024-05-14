<img src="file/img/logo.jpg" width = "315" height = "265" alt="" align="center" />  

# GECAM数据分析工具（GECAMTools）



## 简介  
  GECAMTools是GECAM数据的应用编程接口(API)。本工具基于 python3实现，目的是允许一般用户将GECAM数据分析整合到自己的脚本和工作流中，而不必考虑太多的细节。为此，本工具有高级的API层，允许用户仅用几行代码来读取、简化和可视化GECAM数据。对于专家用户以及希望对其分析的各个方面进行精细控制的用户，本工具提供了一个较低级别的API层。本工具目前已实现数据分析的基本功能，包括时间转换、查看光变、查看能谱、生成响应文件和生成能谱文件用于能谱拟合。  
  此外，GECAMTools的设计有考虑到通用性。本工具的数据接口目前使用的是数据是GECAM数据，可通过继承结构将许多功能推广到其他仪器的数据上。即使数据文件定义与GECAM的文件定义不同,一旦这些数据文件的读取接口被重定义，就可以使用本工具进行后续分析。



  开发人员：  
  张鹏(IHEP)、薛王陈(IHEP)、张艳秋(IHEP)和熊少林*(IHEP)   

  Email:  
  熊少林*(xiongsl@ihep.ac.cn)  
  张鹏(zhangp97@ihep.ac.cn),GECAMTools的安装和使用问题可联系此邮箱反馈。

### GECAM介绍和数据发布网站：[链接](http://gecam.ihep.ac.cn/)<br>  

---
## 使用说明

### 所需环境  
    1 系统环境：windows、linux、mac  
    2 python环境：python版本>=3.6 (不建议安装python 3.9及以上版本)

### 安装流程  
1 下载源程序  
`gecamTools-master.zip`

2 安装  
2.1 仅使用基本功能(即无需生成响应矩阵)  
使用pip进行源码安装，自动安装GECAMTools以及相关依赖库   
`pip install gecamTools-master.zip`    

建议使用Anaconda创建独立的python环境使用，防止出现不同软件的依赖库版本不兼容问题。
[Miniconda使用说明](https://www.jianshu.com/p/7299c2d4d170)<br>  

2.2 使用全部功能(包含生成响应矩阵)   
2.2.1 下载安装GECAM的标定库CALDB  
(1) 下载GECAM-CALDB, 参考已公布的链接:[GECAM-CALDB](http://gecamweb.ihep.ac.cn/xgwd.jhtml)   
(2) 从GECAM集群上下载最新版的CALDB.(截止2022-03-18，最新版本CALDB的路径为：/gecamfs/soft/CALDB)   

    GECAM-CALDB 安装：Linux或Mac     
    (1) 标定库CALDB下载之后, 将source /CALDB path/software/tools/caldbinit.sh 这句话放环境文件里   
    (2) source 环境文件，可进入 python，并通过 `from RSP_Generator import gen_rsp_fits` 来检验标定库是否安装成功

    GECAM-CALDB 安装: Windows (测试于win10):   
    (1) 添加系统变量： 变量名为：CALDB， 地址为CALDB对应的根目录，例：E:\gecam\CALDB   
    (2) 在python环境的site-packages中新建一个CALDB.pth文件
        可通过以下方法找到python或者conda对应的目录：
        >>> import os
        >>> os.path.dirname(os.__file__)
        >>> 'C:\\Users\\用户名\\.conda\\envs\\gecamTools\\lib'
        因此新建文件：C:\Users\用户名\\.conda\envs\gecamTools\Lib\site-packages\CALDB.pth
        CALDB.pth中内容为CALDB中software文件夹路径：E:\gecam\CALDB\software
    (3) 完成之后，可进入 python，通过 `import RSP_generator` 来检验标定库是否安装成功

2.2.2 下载安装HXMT的标定库CALDB(如需分析HXMT的GRB数据)  
(1) 下载HXMT-CALDB, 参考已公布的链接: [HXMT-CALDB](https://ihepbox.ihep.ac.cn/ihepbox/index.php/s/A99tEknkuCbdpsP)   
(2) python环境需额外安装numba库： pip install numba  

    HXMT-CALDB 安装：Linux或Mac     
    (1) 标定库HXMT-CALDB下载之后, 将source HXMT_CALDB path/HXMT_RSP_Generator/tools/hxmt_rsp_generator_init.sh 
    这句话放环境文件里,或直接source  
    (2) source 环境文件，可进入 python，并通过 `from HXMT_RSP_Generator import HXMTrspg_v1` 来检验标定库是否安装成功

    HXMT-CALDB 安装: Windows (测试于win10):   
    (1) 添加系统变量： 变量名为：HXMT_CALDB， 地址为CALDB对应的根目录，例：E:\gecam\HXMT_CALDB  
    (2) 在python环境的site-packages中新建一个HXMT_CALDB.pth文件
        可通过以下方法找到python或者conda对应的目录：
        >>> import os
        >>> os.path.dirname(os.__file__)
        >>> 'C:\\Users\\用户名\\.conda\\envs\\gecamTools\\lib'
        因此新建文件：C:\Users\用户名\\.conda\envs\gecamTools\Lib\site-packages\HXMT_CALDB.pth
        HXMT_CALDB.pth中内容为CALDB的根目录，例：E:\HXMT\HXMT_CALDB
    (3) 完成之后，可进入 python，通过 `from HXMT_RSP_Generator import HXMTrspg_v1` 来检验标定库是否安装成功

2.3 测试  
`import gecam`

### 卸载流程  
`pip uninstall GECAMTools`

---
## 历史版本
### v20240514  
#### 源码和使用手册
[下载方式-IHEPBox](https://ihepbox.ihep.ac.cn/ihepbox/index.php/s/x6HkDidQ8eCvrrG)  

#### 更新说明
<font color="#ff8a14">修复问题：</font><br>
1. 修正时间bin和能谱的源区间浮点数精度导致的时间分解谱时间重叠问题
2. 提升T90计算的稳健性
3. 去除高版本依赖库的限制


### v20230701  
#### 源码和使用手册
[下载方式-IHEPBox](https://ihepbox.ihep.ac.cn/ihepbox/index.php/s/qBd3Djte6MBDYcT)  

#### 更新说明
新增：<br>
1. 新增对于HXMT的GRB数据的分析。 

修复问题：<br>
1. 细节问题修复


### v20230611  
#### 源码和使用手册
[下载方式-IHEPBox](https://ihepbox.ihep.ac.cn/ihepbox/index.php/s/Tqeabem1uhsOrax)  

#### 更新说明
新增：<br>
1. 增加gecam的事例数据根据时间段截取保存的功能(evt.crop)，见2.1.2节。 

修复问题：<br>
1. 修正计算T90时，净光变误差计算错误。
2. 修正多探头叠加的光变只能单独修正死时间：  
    evt.plot_light_curve_with_detectors和evt.plot_spectrum_with_detectors将不再返回叠加后的光变和能谱对象（total_lc_obj和total_spec_obj）。
3. 修正能谱错误（计数为整数）。
4. 总光变自动修正死时间（此调整不影响能谱）。  
events.to_light_curve和lc_kwargs_dic中的参数correct_by_dead_time无效，都会修正死时间，只是总光变在取出数据（get_data, get_plot_data）时增加correct_by_dead_time来提取是否修正死时间的光变数据。
5. 修正画图错误。 
6. 细节问题修复




### v20230420 
#### 源码和使用手册
[下载方式-github](file/source_code/v20230420/)  
[下载方式-IHEPBox](https://ihepbox.ihep.ac.cn/ihepbox/index.php/s/vSA1yPTQBSUF2Pt)  

#### 更新说明
<font color="#ff8a14">修复问题：</font><br>
1. 修复evt中生成多探头光变的误差计算错误<br>
2. 修正并道数据设置channel bin失效的问题<br>
3. 能谱图中总谱、本底谱和净谱统一为修正死时间后的能谱，统一能谱为counts/s<br>
4. T90计算异常的问题<br>
5. GECAMC的入射角计算错误。

<font color="#12CF6A">新增：</font><br>
1. 新增各类型文件的统一函数用于(GECAM的事例数据、GECAM的并道数据)：多探头的画光变、画能谱、生成能谱文件、计算T90<br>
    新增函数：<br>
    evt.plot_light_curve_with_detectors<br>
    evt.plot_spectrum_with_detectors<br>
    evt.generate_spec_file_with_detecotrs<br>
    duration_obj.generate_net_light_curve_with_detectors<br><br>
    同时，原始函数将停止更新，过几个版本后删除<br>
    原始函数如下所示：<br>
    evt.plot_light_curve<br>
    evt.plot_spectrum<br>
    evt.generate_spec_file<br>
    duration_obj.generate_net_light_curve_with_detectors<br>
    cal_net_light_curve_cumsum<br>

2. 新增自定义光变用于计算T90，不限于GECAM的数据

