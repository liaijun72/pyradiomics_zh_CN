# PyRadiomics 中文文档


这是一个开源的，用于从医学影像中提取影像组学特征的Python软件包。通过该软件包，我们致力于建立一个标准的影像组学分析流程，同时提供一个可测试的、持续开放的平台，用于简易的、可重复的影像组学特征提取。通过这种方式，我们希望引起（大家）对影像组学功能的注意，并拓展相关社区。该平台支持以2D和3D模式提取特征，可以基于ROI感兴趣区（segment-based）计算其中每一种特征的具体数值，或生成特征图谱feature maps（voxel-based）。

如果你利用该软件包发表了任何工作，请参考索引：

van Griethuysen, J. J.M., Fedorov, A., Parmar, C., Hosny, A., Aucoin, N., Narayan, V., Beets-Tan, R. G. H., Fillon-Robin, J. C., Pieper, S.,Aerts, H. J. W. L. (2017). Computational Radiomics System to Decode the Radiographic Phenotype. Cancer Research,77(21), e104–e107. ‘https://doi.org/10.1158/0008-5472.CAN-17-0339 <https://doi.org/10.1158/0008-5472.CAN-17-0339>‘_

Note: 本研究由美国国家癌症研究所资助5U24CA194354，QUANTITATIVE RADIOMICS SYSTEM DECODING THE TUMOR PHENOTYPE。


Warning：不可用于临床。


# Chapter 1 加入社区！

通过[谷歌小组](https://groups.google.com/forum/#!forum/pyradiomics)加入PyRadiomics社区。


# Chapter 2 Table of Contents目录

## 2.1 Installation 安装

你可以通过三种方式使用Pyradiomics：
+ 1、通过pip安装；
+ 2、通过源安装；
+ 3、通过3D Slicer Radiomics拓展使用；
+ 4、通过pyradiomics Docker使用。

### 2.1.1 1. Install via pip 通过pip安装
通过pip在PyPi上可以获取预编译二进制文件进行安装。在以下提到过的python版本中，对于发布的任一版本的PyRadiomics，程序均可自动安装，而无须其它额外的编译工作。对与其它python版本，也有分布源可以获取，但是需要编译C语言拓展。

+ 确保你的设备中已经安装以下版本的python:3.5,3.6,3.7（64位）。
+ 安装PyRadiomics。

  ~~~ 
  python -m pip install pyradiomics
  ~~~

### 2.1.2 2. Install via conda 通过conda安装
除了通过PyPi上的预编译二进制文件，PyRadiomics也可以通过conda云安装。若通过Conda安装PyRadiomics，运行以下代码：

  ~~~
  conda install -c radiomics pyradiomics
  ~~~

### 2.1.3 3. Install from source 通过源安装
PyRadiomics也可通过源代码安装。通过这种方式，你可以使用最新版本的PyRadiomics，但由于Pyradiomics需要使用C语言拓展计算纹理特征矩阵以及一些形态特征，所以需要为python进行编译设置。

+ 确保你的设备中安装有版本控制系统git。
+ 确保你的设备中安装有python，至少3.5以上（64位）。
+ 复制存储库
    ~~~
    git clone git://github.com/Radiomics/pyradiomics
    ~~~
+ 对于unix系统（MacOSX，linux）:
    ~~~
    cd pyradiomics
    python -m pip install -r requirements.txt
    python setup.py install
    ~~~

    - -为了交互使用和开发使用组件
    ~~~    
    python setup.py build_ext --inplace
    ~~~
    - -如果你没有sudo/admin权限，你需要在本地安装numpy,nose,tqdm,PyWavelets,SimpleITK(已在requirements.txt中指定)。在bash shell输入：
    ~~~
    pip install --user --upgrade pip
    export PATH=$HOME/.local/bin:$PATH
    pip install --user -r requirements.txt
    export PYTHONPATH=$HOME/.local/lib64/python2.7/site-packages
    ~~~
+ 对于Windows系统：
    ~~~
    cd pyradiomics
    python -m pip install -r requirements.txt
    python setup.py install
    ~~~
+ 如果安装失败，请参考Frequently Asked Questions常见问题解答。如果你的问题不在清单上，请在PyRadiomics Github上创建问题联系我们。

### 2.1.4 4. Use 3D Slicer Radiomics extension 通过3D Slicer 影像组学拓展模块使用
3D Slicer是一个用于医疗影像计算的开源研究平台。可在此处了解和下载3D Slicer软件包：http://slicer.org.

安装后，你可以使用3D Slicer Extension Manager 来安装影像组学拓展模块，通过该模块可以以图形交互方式使用pyradimics。通过3D Slicer使用pyradiomics的优势在于，你可以观察影像和分割，你可以导入已存在的分割并确认他们的质量，或利用3D Slicer中的多种工具来调整你的分割。

更多有关3D slicer Radiomics 拓展安装的细节介绍参考以下地址：https://github.com/Radiomics/SlicerRadiomics

### 2.1.5 5. Use pyradiomics Docker 通过pyradiomics Docker使用
如果你有兴趣使用命令行来使用pyradiomics，推荐使用该方法，但在你的系统中安装软件包时可能会遇到困难。

首先，你需要在你的系统中安装Docker。你可以参考以下操作步骤：

Docker安装后，你可以在shell中输入docker pull radiomics/pyradiomics : CLI来下载 pyradiomics Docker image。然后你可以通过以下方式唤起pyradiomics工具：

~~~
docker run radiomics/pyradiomics : CLI --help
~~~

Docker containers不能直接访问主机上的文件系统。为了将文件作为参数向pyradiomics传递，以及获取转换器创立的文件，需要额外使用-v参数指定用以进行文件交互的文件夹地址：

~~~
-v <HOST_DIR>:<CONTAINER_DIR>
~~~

该参数会允许存储器在CONTAINER_DIR位置上与HOST_DIR路径进行链接。Docker contanier转换器可以通过引用CONTAINER_DIR路径读写文件。

### 2.1.6 Setting up Docker 设置Docker
Docker（http://docker.com）是在软存储器内部自动化部署应用的项目。Docker应用是包含所有初始化应用组分和步骤的_images_实例。一个_container_即是一个image运行实例。我们提供了一个包含编译好的pyradiomics库的image实例，在docker/pyradiomics:CLI。通过使用pyradiomics Docker container你可以在任何支持Docker的电脑上使用Pyradiomics而无须编译pyradiomics。你所需要做的就是在你的系统上安装Docker，然后下载pyradiomics Docker image。

首先你需要通过如下操作步骤在你的系统中安装Docker。Docker 可在Mac，Windows以及Linux系统中安装。大多数情况下，安装Docker很简单，但在Windows系统中,需按如下讨论的内容进行额外设置。

**如果你在Windows系统中使用Docker...**

系统需求

+ Windows 10 Pro或以上。

+ Hyper-V 软件包（Docker会进行提示）。

+ 虚拟机。阅读[此处](https://docs.docker.com/desktop/troubleshoot/overview/#virtualization-must-be-enabled)学习如何检查虚拟机是否打开，如果没有，这里有一份[指南](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/virtualization/sect-virtualization-troubleshooting-enabling_intel_vt_and_amd_v_virtualization_hardware_extensions_in_bios)可以帮助你，但是首先你得确认你可以进入你的BIOS设置。

IMPORTANT：你同样需要在以下屏幕截图中所示的Docker Settings中,共享你用于与Docker image传输数据的驱动器。

大概率你可能会遇见与如下所示类似的错误提醒：

~~~
C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon:
C: drive is not shared. Please share it in Docker for Windows Settings.
See 'C:\Program Files\Docker\Docker\Resources\bin\docker.exe run --help'.
~~~

如果你遇到了该错误，请确保HOST_DIR所在的驱动器，已经设置了（文件）共享：
1. 在Docker任务栏按钮上右键并选择“Settings”
2. 在左侧的菜单中选择“Shared Drives”（可看到一系列可用于共享的驱动器列表）
3. 选择HOST_DIR所在的驱动器进行共享
4. 点击Apply确认并继续。

## 2.2 Usage 使用
### 2.2.1 Instruction Video 视频介绍
### 2.2.2 Example 案例

+ PyRadiomics案例代码和数据保存于[Github repository](https://github.com/AIM-Harvard/pyradiomics)中

+ 案例数据保存在pyradimics/data文件夹中

+ 使用jupyter运行helloRadiomics的案例，位于pyradiomics/notebooks文件夹中。

+ Jupyter同样可以运行视频介绍中的案例。
    - 案例笔记保存于pyradiomics/notebooks文件夹中。
    - 在视频介绍中使用的参数配置文件parameter file保存于pyradiomics/examples/exampleSettings中。

+ 如果没有安装jupyter，作为替代，可运行保存在pyradiomics/examples文件夹中python脚本：
    ~~~
    - python helloRadiomics.py # (segment-based 提取)

    - python helloVoxel.py # (voxel-based 提取)
    ~~~

### 2.2.3 Voxel-based extraction Voxel-based提取
在2.0版本中，pyradiomics引入了voxel-based提取。通过命令行代码以及交互方式均可使用。阅读获悉更多细节。

重要提示，这种提取方式会耗费更多的时间（需要为每一个voxel计算特征值），并且结果会生成Simple ITK影像构成的feature maps特征图谱，而不是一系列特征数值。

### 2.2.4 Command Line Use 命令行使用方法
经由节点pyradiomics进入后，可通过命令行的方式直接使用PyRadiomics。基于输入的内容，PyRadiomics可使用单一（影像）特征提取方式和批量（影像）特征提取方式。通过以下命令查询可以使用的命令清单：

~~~
pyradiomics -h
~~~


**Single image/mask 单个image影像/mask掩膜**

从单个image影像和segmentation分割中提取影像特征，可运行如下代码：

~~~
pyradiomics <path/to/image> <path/to/segmentation>
~~~


**Batch Mode 批量模式**

批量提取影像组学特征：

~~~
pyradiomics <path/to/input>
~~~

该模式中输入的文件格式，应该是CSV文件类型的，并且文件中第一“行”’为标头，之后的每一“行”为image影像和segmentation分割的组合，至少包含两个内容：1) path/to/image（影像文件的路径）, 2)path/to/mask（掩膜文件的路径）。第一行标头中必须分别以“Image”指定代表影像文件的“列”，以“Mask”指定代表掩膜的“列”（注意大小写）。也可指定添加多余的列，这些列的内容会按照相同的顺序输出到结果中（计算出的特征结果会在最后的“列”之后附加）。用“Label”列指明从某一影像和分割中提取特征使用的自定义数值。在该“列”中设置的值执行优先级在parameter file参数配置文件或命令行之上。如果某一“行”中没有数值，会采用默认（或全局参数）数值。同样的，可以使用“Label_channel”列来指定label_channel参数。

Note：所有标头必须是独一无二的，且与PyRadiomics(\<filter>\_\<class>\_\<feature>)中提供的标签不同。如果冲突，其中的值会被PyRadiomics中的值覆写。

Note：在批量模式中，可以使用多线程方式加速。这发生于案例水平上（i.e.每一线程处理一个案例）。可以通过指定--jobs参数，来指定需要多少个平行线程来运行。


**Customization 定制**

特征提取可以通过--param参数指定一个*parameter file*参数配置文件，或者通过优先级更高的--setting参数来进行自定义设置（仅type3 customization）。可以多次使用--setting参数来进行多重覆写。

**Output 结果**

默认情况下，结果会输出至控制台窗口。可以通过使用-o \<PATH>以及-f csv参数将文件保存至CSV格式文档中，其中\<PATH>用于指定文件保存的位置。e.g:

~~~
pyradiomics <path/to/image> <path/to/segmentation> -o results.csv -f csv
pyradiomics <path/to/input> -o results.csv -f csv
~~~

**Voxel-based Radiomics Voxel-based影像组学**

通过添加参数--mode voxel提取feature maps特征图谱（voxel-based 提取）。计算后的结果会在当前目录下以影像（NRRD格式）形式保存，命名方式为 “Case-\<idx>_\<FeatureName>.nrrd”。可以通过--out-dir的命令行改变输出文件夹。在控制台窗口展示的结果以及输出的文件中会保留diagnostic information特征信息，提取的特征的数值会锚定在相应的位置上在feature maps特征图谱中保存。

### 2.2.5 Interactive Use 交互使用

+ （LINUX）通过源代码运行，需要将pyradiomics添加至PYTHONPATH变量环境中（如果已安装PyRadiomics则不需要）：
    ~~~
    – setenv PYTHONPATH /path/to/pyradiomics/radiomics
    ~~~
+ 启动python 交互进程：
    ~~~
    - python
    ~~~
+ 导入必要的类。
    ~~~
    import os

    import SimpleITK as sitk
    import six

    from radiomics import featureextractor, getTestCase
    ~~~

+ 设置pyradiomics运行目录。
    ~~~
    dataDir = '/path/to/pyradiomics'
    ~~~

+ 你会发现案例文件brain1_image.nrrd 和 brain1_label.nrrd在相应的目录中。注意，此处并不意味着你的文件必须是NRRD格式。任何可通过ITK阅读的格式均可（e.g., NIfTI, MHA, MHD, HKR, etc）。更多细节参照常见问题答疑中相关的部分。

+ 通过两个变量存储image影像和mask掩膜的文件路径。
    ~~~
    imageName, maskName = getTestCase('brain1', dataDir)
    ~~~
+ 同样的，（用变量）存储包含提取设置配置文件的路径。
    ~~~
    params = os.path.join(dataDir, "examples", "exampleSettings", "Params.yaml")
    ~~~
+ 通过parameter file参数配置文件设置特征提取器。
    ~~~
    extractor = featureextractor.RadiomicsFeatureExtractor(params)
    ~~~
+ 计算特征（segment-based）：
    ~~~
    result = extractor.execute(imageName, maskName)

    for key, val in six.iteritems(result):

        print("\t%s: %s" %(key, val))
    ~~~

+ 计算特征（voxel-based）
    ~~~
    result = extractor.execute(imageName, maskName, voxelBased=True)

    for key, val in six.iteritems(result):

        if isinstance(val, sitk.Image):# Feature map

            sitk.WriteImage(val, key + '.nrrd', True)

            print("Stored feature %s in %s" % (key, key + ".nrrd"))

        else:# Diagnostic information

             print("\t%s: %s" %(key, val))
    ~~~
+ 阅读 [feature extractor class特征提取类](#241-feature-extractor-特征提取器) 获取有关该核心类的更多信息。


### 2.2.6 3D Slicer中的PyRadiomics
我们提供一个便捷的可在前端交互使用的3D Slicer“Radiomics”拓展，点击[这里](https://github.com/AIM-Harvard/SlicerRadiomics)获取。

### 2.2.7 Setting Up Logging 设置Logging记录

Logging记录用以追踪特征提取过程中的问题。默认情况下，PyRadiomics logging记录报告WARNING及以上级别的信息（报告任何warnings提醒或发生的errors错误），并将该信息输出至结果中。默认情况下，PyRadiomics不产生log记录文件。

通过交互使用setVerbosity()命令或调整命令行中的可选参数--verbosity，调整结果中出现的信息的数量，。

当采用交互模式使用RyRadiomics时，通过添加适当的处理器到PyRadiomics logger记录器中，可以将PyRadiomics logging记录信息存储到一个文件中。

~~~
import radiomics

log_file = 'path/to/log_file.txt'
handler = logging.FileHandler(filename=log_file, mode='w')  # overwrites log_files from previous runs. Change mode to 'a' to append.

formatter = logging.Formatter("%(levelname)s:%(name)s: %(message)s")  # format string for log messages

handler.setFormatter(formatter)
radiomics.logger.addHandler(handler)

# Control the amount of logging stored by setting the level of the logger. N.B. if the level is higher than the Verbositiy level, the logger level will also determine the amount of information printed to the output

radiomics.logger.setLevel(logging.DEBUG)
~~~

通过命令行使用pyradiomics时，通过可选参数--log-file指定存储log file记录文件的位置。存储信息的数量可以通过--logging-level参数来进行控制（默认为WARNING及以上级别）。

## 2.3 Customizing the Extraction 自定义提取
### 2.3.1 Types of Customization 设置方式

PyRadiomics提供4种方式以进行自定义特征提取：

+ Type1 指定用以特征提取的image类型（原生/派生）
+ Type2 指定提取的特征（类别）
+ Type3 指定设置，用以控制预处理以及使用的滤波和特征类别
+ Type4 指定voxel-based专项设置，仅在利用PyRadiomics生成feature maps特征图谱时可以使用

Warning：在初始化特征提取器或某一特征类别时，可以在相应的**kwargs关键词参数中进行设置。此处仅包含type3类型的参数。使用parameter file参数配置文件控制type1（影像类型image type）和type2（feature class特征类别）仅可在（特征提取器）初始化时进行设置。如果不使用parameter file参数配置文件，或需要在初始化之后更改参数，则需分别调用相应的函数。

#### **2.3.1.1 Image Types 影像类型**

支持基于多种Image Types（原生的或派生的）进行影像特征提取。会动态识别支持的Image Types（通过imageoperations.py中用于匹配image type标签的函数实现）。

激活的types类型存储在特征提取类实例中的_enabledImageTypes字典中，可通过enableAllImageTypes(), disableAllImageTypes(), enableImageTypeByName() 和enableImageTypes()函数进行调整。也可为每一激活的Image Type提供自定义设置，以在针对此image type影像类型进行特征提取时应用。请注意，这仅仅在某一滤波应用时或之后生效（i.e.并不是在特征提取器水平）。

Note：这种定制方式可以在Parameter File参数配置文件中，利用imageTpye关键词进行设置。

Note：默认情况下，只有“Original” Image Type被激活。

当前支持的Image Types 影像类型包括：

+ Original：没有使用滤波。

+ Wavelet：wavelet滤波，在每一水平上产生8个分解（在三维中任一维度上，使用高通滤波或低通滤波产生的所有结果的组合。详见getWaveletImag()）

+ LoG：Laplacian of Gaussian滤波，边缘增强滤波。强调灰度强度变化的区域，通过sigma调整显示的纹理粗糙的程度。低sigma值突出细致的纹理（在短距离内（灰度）发生变化），高sigma值突出粗糙的纹理（在长距离内（灰度）发生变化）。详见getLoGImage()。

+ Square：计算影像强度的平方并线性刻画至本来的范围。如果本来图像中为负值，则数值平方后会重新调制为负值。

+ SqureRoot：计算影像强度绝对值的平方根并线性刻画至本来的范围。如果本来图像中为负值，则数值求平方根后会重新调制为负值。

+ Logarithm：计算绝对值+1的对数。并调制至本来的范围，如果原始值为负数，则计算后的数值也会调制为负数。

+ Exponential：计算幂函数。并调制至本来的范围，如果原始值为负数，则计算后的数值也会调制为负数。

+ Gradient：计算局部梯度。详见getGradientImage()。

+ LocalBinaryPattern2D：基于切片方式（2D）计算Local Binary Pattern。详见getLBP2DImage()。

+ LocalBinaryPattern2D：基于3D使用球谐函数计算Local Binary Pattern。详见getLBP3DImage()。

#### **2.3.1.2 Enabled Features 可提取的特征**

支持从多种类型（原生或派生）的影像中提取多种特征。可提取的特征是动态识别的，按顺序保存在特征类中。了解更多用于识别特征及特征类的标签，请阅读Develpoers部分。

可提取的特征以_enbledFeatures字典的形式储存于特征提取类实例中，可通过enableAllFeatures()，disableAllFeatures()，enableFeatureClassByName()以及enableFeaturesByName()函数进行调整。字典中的每一键值对，其中"键"用以代表feature class特征类别，“值”用以代表一系列（该类别下）可提取的feature names特征名称。如果值为None，或为空列表。则该类别中所有特征均默认提取。其它情况下仅提取指定的特征。

Note：这种自定义方式可以在Parameter File参数配置文件中，通过使用featureClass关键词进行设置。

Note：默认情况下，提取所有特征类型及全部特征。

当前支持提取的feature classes特征类别包括：

+ firstorder

+ shape

+ glcm

+ glrlm

+ glszm

+ gldm

+ ngtdm

提取某一特征可以传入，命名该特征函数所使用的独一无二的标签。（e.g. get10PercentileFeatureValue() 定义的first order 特征，可以通过{firstorder: \['10Percentile']}这种方式激活）。在Radiomic Features影像组学特征部分可查阅所有函数标签。

#### **2.3.1.3 Settings 设置**

除了自定义提取的内容（Image types，features）,PyRadiomics提供多种方式设置如何提取特征。这些设置在不同的水平发挥作用。E.g. 重采样仅仅发生在影像导入（特征提取器）之后，因此重采样设置仅发生在特征提取水平上。设置（内容）以setttings字典形式存储于特征提取器实例中，（字典中的）键代表相应设置的名称。在特征提取器启动时可以通过输入关键词参数（以设置名称为“关键词”，具体参数值为“值”，e.g. binWdith=25）进行设置，或者以settings字典形式进行设置。

Note：这种定制方式可以在Parameter File参数配置文件中，通过setting关键词进行设置。

Note：当直接使用feature classes特征类时，特征类水平的设置可以在特征类初始化时通过提供关键字参数进行设置。

以下是控制特征提取操作的设置，以层次水平和类别排序。每一项设置均以独一无二，大小写敏感的名称命名，其后方括号中是该设置的默认值。默认值之后是默认值的类型，以及该设置的（说明）文档。

**Feature Extractor Level 特征提取器水平**

*Image Normalization  图像标准化*

+ normalize [False]: Boolean，布尔值，设置为Ture会在重采样前对影像进行标准化操作。也可参阅normalizeImage()
+ normalizeScale [1]: Float，浮点数值，>0，控制图像标准化后的比例。如果没有使用标准化，该设置不产生影响。
+ removeOutliers [None]: Float，浮点数值，>0，定义从图像中移除的异常值。异常值定义为与平均值相差𝑛 𝜎𝑥倍标准差的数值，其中n>0，并等于该设置使用的数值。如果未设置该参数（在参数配置文件parameter file中未设置该数值或空值会导致错误），则不会排除异常值。如果未进行标准化，该设置不会产生影响。也可参阅normalizeImage()。

*Resampling the image/mask 图像/掩膜重采样*

+ resampledPixelSpacing [None]: List of 3 floats (>= 0)，3个浮点数值构成的列表，设置voxel重采样时在（x,y,z）水平上的大小。设置为0代表在image影像或mask掩膜的某一维度上使用本来的数值（即不进行重采样）。例如，在平面尺度上进行重采样，则仅需编辑x和y的数值（e.g.:[2,2,0]）。对平面的解析与影像获取的角度有关（i.e. 横轴位，冠状位，矢状位）。

+ interpolator [sitkBSpline]: SimpleITK常量或字符串名称，用以指明重采样时使用的插值器interpolator。指定的interpolator仅用对image影像进行重采样，对mask掩膜重采样则使用sitkNearestNeighbor以保留标签数值。可采用的值列举如下：

        – sitkNearestNeighbor (= 1)

        – sitkLinear (= 2)

        – sitkBSpline (= 3)

        – sitkGaussian (= 4)

        – sitkLabelGaussian (= 5)

        – sitkHammingWindowedSinc (= 6)

        – sitkCosineWindowedSinc (= 7)

        – sitkWelchWindowedSinc (= 8)

        – sitkLanczosWindowedSinc (= 9)

        – sitkBlackmanWindowedSinc (= 10)

+ padDistance [5]: Integer，整数值，≥0，设置重采样时围绕切割的肿瘤体积周围填充的voxels数量的多少。Padding填充于所有表面且发生在新的特征空间上。i.e. 在x, y, z方向上均以2*padDistance的大小增长。对于某些滤波需要设置填充padding（e.g. LoG）。填充的voxels的灰度强度与原本的灰度强度相当，且填充不会超过本来影像的边界。N.B.应用滤波后，影像会重新进行（ROI）分割且不进行填充。

注意：当resampledPixelSpacing或interpolator设置为None时，会关闭重采样。

*Pre-Cropping 预裁切*

+ preCrop [False]: Boolean，布尔值。如果设置为True，并且关闭重采样，会沿边框裁切影像，并以指定的padDistance值进行填充。与重采样后进行padding填充类似，预切割后的padding填充不会超过本来图像的边界。设置preCrop为True可以加速（特征）提取和占用更少的内存，尤其在影像很大而ROI很小的情况下。

Note：由于image影像和mask掩膜在传递至feature classes特征类之前也会沿边框进行裁切，因此预裁切仅在使用滤波时有益。

*Resegmentation 再分割*

+ resegmentRange [None]: 1~2个浮点数值的构成的列表，分别指定最低及最高（可选）的阈值。超过该范围的voxels会在特征计算前从mask掩膜中移除。如果该值为空值（默认即空值），则不会进行再分割。再分割后的大小会进行检查（通过minimumROISize，默认为1），如果失败，会记录错误，该案例的特征提取操作会被跳过。

+ resegmentMode [‘absolute’]: string，字符串，用以说明再分割阈值确定的方法。

    absolute：resegmentRange值以绝对值对待。i.e. 即（直接依据数值）直接进行再分割。

    relative：resegmentRange值以ROI中的最大值的相对值对待。i.e. 实际阈值为threshold = value * 𝑋𝑚𝑎x

    sigma： resegmentRange值以偏离ROI中灰度平均值的标准差的大小界定。E.g. 为了排除超过平均值3个sigma大小的异常值，指定模式为’sigma’，边界为[-3，3]。阈值定义为threshold = 𝜇 + value * 𝜎.

+ resegmentShape [False]: Boolean，布尔值。如果设置为Ture，则再分割的掩膜同样用于shape特征计算。如果设置为False，则只有first order 以及texture class 特征会使用再分割的掩膜进行计算（在IBSI中即强度掩膜）。Shape特征会在使用重采样（可选）和矫正后的掩膜上进行计算（在IBSI中即形态掩膜）。

*Mask validation  掩膜验证*

+ minimumROIDimensions [2]: Integer，整数值 范围1-3，指定最小的维度（分别代表1D，2D，3D），不包括单个体素的分割。

+ minimumROISize [None]: Integer，整数值，＞0，指定所需的最少voxels数目。如果省略了该数值，会直接跳过检测。（在parameter file参数配置文件中设置为None会导致错误）。

+ geometryTolerance [None]: Float，浮点数值，说明使用SimpleIKT比较image影像和mask掩膜的原点，方向和空间分辨率（的差异）时可容忍的程度。影响checkMask()的第一步。如果设置为None，PyRadiomics会采用SimpleITK使用的默认值（1e-16）

+ correctMask [False]: Boolean，布尔值，如果设置为True，PyRadiomics会在第一步checkMask()失败时，尝试依据image的形状对mask掩膜进行重采样。这种方法使用的是最近邻插值器。如果mask掩膜中的ROI超过image影像的物理边界，掩膜检测会继续失败。

*Miscellaneous 附加信息*

+ additionalInfo [True]: boolean，布尔值，设置为False可以关闭额外的信息出现在提取结果中。也可参阅addProvenance()。

**Filter Level 滤波水平**

*Laplacian of Gaussian settings*

+ Sigma：浮点数值或整数值构成的列表，必须大于0。滤波使用的sigma数值（调整显示粗糙的程度）。

Warning：如果激活LoG滤波，则必须设置sigma数值。如果省略，则不会计算任何LoG image影像特征，会返回一个空字典。

*Walelet setings*

+ start_level [0]: integer，整数值，计算某一个标签时，产生的首个分解集合的0基础wavelet水平.

+ level [1]: integer，整数值，计算某一个标签时，wavelet分解水平的数量

+ wavelet [“coif1”]: string，字符串，wavelet分解的类型。在pyWavelet.wavelist()列举了合理的取值。当前支持的取值（pywavelet version 0.4.0）（需要额外数字的，数值的范围在[]中声明）：

        – haar

        – dmey

        – sym[2-20]

        – db[1-20]

        – coif[1-5]

        – bior[1.1, 1.3, 1.5, 2.2, 2.4, 2.6, 2.8, 3.1, 3.3, 3.5, 3.7, 3.9, 4.4, 5.5, 6.8]

        – rbio[1.1, 1.3, 1.5, 2.2, 2.4, 2.6, 2.8, 3.1, 3.3, 3.5, 3.7, 3.9, 4.4, 5.5, 6.8]

*Gradient settings*

+ gradientUseSpacing [True]: Boolean，布尔值，如果设置为True，计算影像梯度时会考虑影像的空间分辨率。

*Local Binary Pattern 2D*

+ lbp2DRadius [1]: Float，浮点数值，＞0，用于指明采样时判定相邻单位的尺度。
+ lbp2DSamples [9]: Integer，整数值，≥1，指定用于采样时样本的数量。
+ lbp2DMethod [‘uniform’]: String，字符串，指定计算LBP时使用的方法。

Warning：需要skimage软件包。

*Local Binary Pattern 3D*

+ lbp3DLevels [2]: integer，整数值，≥1，指定使用的球谐函数中水平的数量。
+ lbp3DIcosphereRadius [1]: Float，浮点数值，>0，用于指明采样时判定相邻单位的尺度。
+ lbp3DIcosphereSubdivision [1]: Integer，整数值，≥0，用于指定在正多面体中应用的细分部的数量。

Warning：需要scipy 和trimesh软件包。

**Feature Class Level  特征类水平**

+ Label [1]: Integer，整数值，说明labelmap标图中ROI区域的标签值。

*Image discretization  图像离散化*

+ binWidth [25]: Float，浮点值，＞0，指定对影像中的灰度进行离散化，制作灰度直方图时，采用bins箱距（即分组间距）的大小。
+ binCount [None]: integer，整数值，＞0，指定创造多少个bins分组。（设置后）分组间距由ROI（灰度值）的范围决定。没有明确的证据表明哪种设置方法更好，我们推荐使用了一个固定的分组间距，详见常见问题解答。

*Forced 2D extraction 强制2D提取*

+ force2D [False]: Boolean，布尔值，设置为True，强制进行基于切片的纹理计算。切片的维度由force2Ddimension确定。如果输入的ROI已经是一个2D ROI，则自动进行2D 特征计算。
+ force2Ddimension [0]: int，整数值，0-2之间，指定基于切片进行纹理特征计算时的维度。0代表采用影像的默认维度（通常CT为横轴面，MRI为冠状面或矢状面）。1代表超出平面的y向维度（e.g. 对于横轴位的影像即冠状平面），2代表超出平面的x维度（e.g. 对于横轴位的影像即前后向平面）。如果force2D设置为False，则该处的设置不会发生作用。

*Texture matrix weighting 纹理矩阵权重*

+ weightingNorm [None]: string，字符串，指定在衡量距离时使用的标准。可参考的设置如下。

        – ‘manhattan’: 一阶范数

        – ‘euclidean’: 二阶范数

        – ‘infinity’: 无穷范数 

        – ‘no_weighting’: GLCMs采用因子1权重并求和

        – None: 不采用权重，返回基于单独的矩阵计算的平均值

    对于提供的其它数值，会记录warning，同时会采用“no_weighting”权重。


Note：仅GLCM和GLRLM特征类受此（设置）影响。此外，在这些类中权重的使用方法并不相同。想了解更多有关权重的设置方法，参见GLCM和GLRLM文档。

*Distance to neighbour*

+ distances [[1]]: List of integers，整数值构成的列表。用于衡量沿某一角度，中心voxel及其相邻voxel间的距离。

Note：仅影响GLCM 和NGTDM特征类。GLSZM和GLRLM特征类使用固定距离1（无穷范数）来定义近邻。

**Feature Class Specific Settings 特定Feature Class 专用设置**

*First Order* 
+ voxelArrayShift [0]: Integer，整数值，计算Energy，Total Energy 和RMS时，这个数值会在灰度强度上添加以避免负数。如果使用CT影像，或数值没有经过平均数0标准化，建议将该参数设置为固定的数值（e.g. 2000），这可以确保在影像中没有负数。请牢记，该数值越大，体积混杂效应影响越大。

*GLCM* 
+ symmetricalGLCM [True]: boolean，布尔值，用于说明是否在某一角度的两个方向上衡量共生对，（如果采用）其结果为对称矩阵，对于i和j具有相同的分布。GLCM的对称矩阵基于Haralick et al等人的定义。

*GLDM* 
+ gldm_a [0]: float，浮点数值，α为判定（两个灰度）相关时采用的阈值。与灰度水平为i的中心voxel相邻的灰度水平为j的voxel，应符合|𝑖 − 𝑗| ≤ 𝛼


#### **2.3.1.4 Voxel-based specific settings  Voxel-based 专用设置**
当使用PyRadiomics产生feature maps特征图谱时，存在一些额外的可选设置。这些设置控制用于计算的邻域voxel之间的距离，以及背景值。i.e.比如不需要计算的voxel的某些数值。

+ kernelRadius [1]: integer，整数值，定义距离中心voxel的半径，指定使用的kernel的大小，。实际尺寸为2 * kernelRadius + 1。E.g. 设置1，实际大小为3*3*3，设置2，实际大小为5*5*5。在2D提取中，生成的kernel同样为2D形状。（平面而非立方体）
+ maskedKernel [True]: boolean，布尔值，说明是否利用总体的掩膜掩盖kernel。如果Ture，则仅被掩膜分割到的kernel中的voxels会用于计算。否则，所有kernel中的voxels都会用于计算。并且，如果设置True，会基于ROI进行灰度离散化操作，如果设置为False，则基于整张影像。
+ initValue [0]: float，浮点数值，ROI外使用的voxels的数值，或计算失败的voxels的数值。如果设置为nan，3D切片会视其为透明的voxels。
+ voxelBatch [-1]: integer，整数值，＞0，控制在同一批次中用于计算的voxels最大数量。更大的批量意味着Python中更少的循环，会更快的完成特征提取，但是会需要更多的内存。该设置允许使用者在提取速度和内存使用间进行均衡。如果使用该设置，数值应设置＞0，如果不设置则采用默认数值-1（意味着所有voxels在同一批次中进行计算）

### 2.3.2 参数文件

四种自定义设置的方式，可通过一个单独的yaml或JSON结构文档进行设置，并在命令行中执行pyradiomics时通过可选参数（--param）传入。在交互模式下，也可在feature extractor初始化阶段传入，或在初始化之后通过loadParams()传入。这可以避免上述在Python脚本中通过硬编码的方式进行设置。我们鼓励使用者在pyradiomics存储库中分享这些parameter files参数配置文件。阅读Submitting a parameter file了解更多有关如何传递参数配置文件的信息。

Note：了解设置详单，参阅Images Types, Feature Classes以及Settings。这些设置在参数配置文件中可分别通过关键词imageType, featureClass 和 setting进行设置。

Note：参数配置文件的案例储存在pyradiomics/examples/exampleSettings文件夹中。

参数配置文件依照YAML协定（www.yaml.org）撰写，并会经代码检查以保证一致性。有且仅需要一个yaml文档。参数配置必须依照上述的自定义设置类别进行组织。在文档中的结构安排参照：

~~~
<Customization Category>:
    <Setting Name>: <value>
...
<Customization Categort>:
...
~~~

可以插入空白行以提高可读性，这些空白行会被无视。也可插入额外的解释说明，在前方以“#”标记，可以在空白行或命令行中插入：

~~~
#This is a line containing only comments
setting: # This is a comment placed after the declaration of the 'setting' category.
~~~

任何关键词，如设置类型或设置名称仅可使用一次。多次输入不会引发错误，但仅最后输入的内容有效。

三种设置类型命名如下：

1. imageType：用以设置提取特征依据的image type影像类型。\<value >采用kwarg参数进行设置（以字典方式）。如果\<value>是一个空字典（'{}'），则不会对输入的影像文件进行任何设置。
2. featureClass：可激活的feature class特征类别，\<value>是一系列可激活的特征字符串名称构成的列表，如果没有指定\<value>或提供的是空列表（'[]'）,则该特征类别所包含所有特征均被提取。
3. setting：用以调整预处理设置或专用设置。如果没有指定任何\<value>，则不会进行任何设置。
4. voxelSetting：用以控制voxel-based（）特征提取的专项设置。E.g. 在参数图谱中使用的kernel的尺寸以及背景值。

示例：
~~~
#This is a non-active comment on a separate line

imageType:
    Original: {}
    LoG: {'sigma' : [1.0, 3.0]} # This is a non active comment on a line with active code preceding it.
    Wavelet:
        binWidth: 10

featureClass:
    glcm:
    glrlm: []
    firstorder: ['Mean','StandardDeviation']
    shape:
        - Volume
        - SurfaceArea

setting:
    binWidth: 25
    resampledPixelSpacing:
~~~

在该示例中，使用了三种image types（“Original”, “LoG” (Laplacian of Gaussian) 以及 “Wavelet”），并为“LoG”（“sigma”）和“Wavelet”(“binWidth”)分别进行了设置。可以看到为“LoG”“Wavelet”设置的方法是一致的。

接下来，有4种特征类别被激活。其中“glcm”和“glrlm”分类中所有可提取的特征均被激活，而在“firstorder”类别中仅有“Mean”和“StandardDeviation”特征被激活，在"shape"类别中仅有“Volume”和“SurfaceArea”被激活。可以看到分别为“firstorder”和“shape”指定可激活特征的方法是一致的。
最后，特别指定两项设置，“binWidth”，设置为25（在指定提取“Wavelet”派生的特征时，会采用10）；“resampledPixelSpacing”，未设置具体数值，相当于采用了python中“None”值。

Note：
+ 在parameters未指定的设置会采用默认数值。
+ 可激活的特征会被参数中设置的特征代替。（i.e. 仅指定的特征/类别会被激活。如果省略了设置featureClass，则所有特征类别和特征均会被激活）。
+ ImageTypes会被参数中设置的类型代替。（i.e.仅被指定的类型会被用于特征提取。如果省略了设置“inputImage”，则仅“Original”影像类型会被用于特征提取，而不会进行任何额外的设置。）

## 2.4 Pipeline Modules 管道模块

这部分文档说明了PyRadiomics流程中不同模块和预处理输入数据的方法。其中包含特征定义的Feature class 模块，在Radiomic Features部分说明。

另外，这部分内容包含了radiomics.generalinfo module的文档，可以在提取结果中提供额外的信息。这部分信息可用于提高结果的可重复性。

最后，这部分内容中还包含了global functions的文档，用以在工具箱（如logging记录及C拓展）和radiomics.base module中发挥作用，以定义和Feature class特征类的交互方式。


### 2.4.1 Feature Extractor 特征提取器

class radiomics.featureextractor.RadiomicsFeatureExtractor(*args, **kwargs)

Bases: object

经包装的类，用于计算影像组学标签的计算器。在初始化阶段和之后，有多种设置可以采用以自定义输出的标签。包括使用哪些特征类别及特征，以及采取哪些预处理操作和采用哪种影像类型（original/或filterd）作为输入。

通过调用execute()功能，基于传入的image和labelmap的组合，进行以上这些设置，生成影像组学标签。可以在一批次中反复调用该函数为所有的image和labelmap组合产生影像组学标签。

在初始化阶段，可以传递一个parameters file参数配置文件（用字符串指向一个yaml或json结构编写的文件），或一个字典来调整所有所需的配置内容（第一层级的关键字包括“setting”，“imageType”，“featureClass”）。这是通过将其作为第一位置参数完成的。如果没有提供任何位置参数，或者参数并非字典形式或字符串指向的不是一个合法的文件（即指向的不是一个合法的parameters file），则会采用默认设置。并且，在初始化阶段，自定义设置（不包括image types 和feature classes设置）可以作为关键词参数传入，方法是将设置名称作为关键词，值作为参数值（e.g. binWidth=25）。在此处的设置会覆盖通过参数文件、字典、和默认进行的设置。了解更多设置和自定义设置方法，参见Customizing the Extraction。


默认情况下，所有特征类别中的所有特征均被激活。而只有Original影像类型被使用（即未采用任何滤波处理）。

addProvenance(provenance_on=True)

    指定在提取过程中是否报告附加信息。这些信息包括工具版本，激活的影像类别以及应用的设置。另外，也提供了有关image影像和ROI的信息，包括原影像的空间分辨率，ROI中voxels的总数目，以及所有ROI中相关的volumes的数量。

    关闭此功能，使用addProvenance(False)。

loadParams(paramsFile)

    导入指定的parameters file参数配置文件以更新设置和激活的特征（类别）以及影像类型。有关参数配置文件的结构，详见Customizing the extraction。

    如果提供的文件不符合要求（i.e. 无法识别的名称或不合理的设定数值），则会引起pykwalify 错误。

loadJSONParams(JSON_configuration)

    导入指定的JSON结构的parameters file参数配置文件以更新设置和激活的特征（类别）以及影像类型。有关参数配置文件的结构，详见Customizing the extraction。

    如果提供的文件不符合要求（i.e. 无法识别的名称或不合理的设定数值），则会引起pykwalify 错误。


execute(imageFilepath, maskFilepath, label=None, label_channel=None, voxelBased=False)

    从导入的影像和掩膜组合中计算影像组学标签。包含以下步骤：
    
        1. 导入image影像和mask掩膜，如果需要，进行标准化/重采样。
        2. 使用checkMack()检验ROI是否合规，此过程会计算和返回边界框。
        3. 如果激活，附加信息会被计算和储存在结果中。（在voxel-based提取中不会）
        4. 在original image上裁切（未经过填充）并计算Shape features。（在voxel-based提取中不会）
        5. 如果激活，依据在resegmentRange中指定的范围，对mask进行重分割。（默认None：即关闭重分割）
        6. 依据_enabledImageTypes指定的image types计算其它特征类别。影像会在滤波处理后裁切至肿瘤掩膜形状（未填充），然后再传入特征类别（以进行计算）。
        7. 计算好的特征以collections.OrderedDict形式返回。


    Parameters
    • imageFilepath – SimpleITK Image, 或指向image文件所在位置的字符串

    • maskFilepath – SimpleITK Image, 或指向labelmap文件所在位置的字符串 

    • label – Integer，整数值, （labelmap文件中）用以提取特征的标签的数值。如果未指定，会使用最后指定的标签，默认标签为1。

    • label_channel – Integer，整数值，当maskFilepath指向的是一个vector pixel type的SimpleITK.Image时，用以索引使用的通道，默认值为0。

    • voxelBased – Boolean，布尔值，默认为 False. 如果设置为true, 会执行voxel-based提取, 否则执行segment-based提取。

    Returns结果

    计算得出的特征标签，以字典形式储存。(“<imageType>_<featureClass>_<featureName>”:value)。如果是segment-based提取，特征值为浮点数值。如果是voxel-based提取，则结果为SimpleITK.Image。（由于）附加信息的类型不同，以字符串形式呈现。


static loadImage(ImageFilePath, MaskFilePath, generalInfo=None, **kwargs)

    导入image和labelmap，并进行预处理。如果ImageFilePath是一个字符串，会将其作为SimpleITK Image文件导入，并将其作为image，如果他已经是一个标准的SimpleITK Image，则直接将其指定为image。其它情况则直接忽视（不进行任何计算）。依据MaskFilePath对mask进行相同的设置。如果需要，一个segmentation object分割对象（i.e. mask volume with vector-image type）会转换为一个labelmap形式（即scalar image type）。数据会强制转换为UInt32格式。参见getMask()。

    如果设置了标准化，则在重采样前首先对影像进行标准化。

    如果设置了重采样，则在指定image和mask后，对image和mask进行重采样并依据掩膜进行裁切（并依据padDistance的设置进行填充）。

    Parameters

    • ImageFilePath – SimpleITK.Image 对象或指向可被 SimpleITK 读取的影像文件的字符串，会被用作image。

    • MaskFilePath – SimpleITK.Image 对象或指向可被 SimpleITK 读取的影像文件的字符串，会被用作mask。

    • generalInfo – GeneralInfo Object对象。如果设置了，会用于存储预处理的附加信息。

    • kwargs – 对特定的影像类型使用的设置组成的字典。

    Returns

    2个Simple.ITK.Image对象，分别代表导入的image和mask.


computeShape(image, mask, boundingBox, **kwargs)

    计算传入的image和mask 的形态（2D和/或3D）特征。

    Parameters

    • image – SimpleITK.Image 对象， 代表使用的image

    • mask – SimpleITK.Image 对象， 代表使用的mask

    boundingBox – checkMask()计算的boundingBox（大小）, i.e. 在相应维度上，由较低（偶数索引）和较高（奇数索引）边界组成的边界框构成的元组。

    • kwargs – 准备使用的设置构成的字典。

    Returns

    经计算产生的形态特征组成的 collections.OrderedDict。如果没有计算特征，则生成一个空的OrderedDict。

computeFeatures(image, mask, imageTypeName, **kwargs)

    基于image, mask 和**kwargs设置计算特征。

    该函数基于传入的image (original or derived)计算特征，不会对传入的影像进行任何预处理或滤波处理。计算的特征/类别定义在self.enabledFeatures中。也可参阅enableFeaturesByName().

    Parameters

    • image – 经过裁切的用于计算的 (可能经过滤波处理的) SimpleITK.Image 对象，代表使用的image。

    • mask – 经过裁切的用于计算的 SimpleITK.Image 对象，代表使用的mask。

    • imageTypeName – 说明对影像进行何种滤波处理的字符串。如果未设置，则执行“original”类型。

    • kwargs – 针对某一特定image type设置内容组成的字典。

    Returns
    经计算产生的所有激活类别的特征组成的 collections.OrderedDict。如果没有计算特征，则生成一个空的OrderedDict。

    Note：形态特征不基于影像灰度（计算），因此单独计算（在execute中）。在这个函数中，不会计算形态特征。


enbleAllImageTypes()

    激活所有支持的Image types，不附加任何设置。

disableAllImageTypes()

    不采用任何imagetypes。

enableImageTypeByName(imageType, enabled=True, customArgs=None)

    采用或不采用指定的image type。如果采用image type，可通过customArgs进行设置。

    当前支持的Image Types包括：

    Original：没有使用滤波。

    Wavelet：wavelet滤波，在每一水平上产生8个分解（在三维中任一维度上，使用高通滤波或低通滤波产生的所有可能组合的结果。详见getWaveletImag()）

    LoG：Laplacian of Gaussian滤波，边缘增强滤波。强调灰度强度变化的区域，通过sigma调整显示的纹理粗糙的程度。低sigma值突出细致的纹理（在短距离内（灰度）发生变化），高sigma值突出粗糙的纹理（在长距离内（灰度）发生变化）。详见getLoGImage()。

    Square：计算影像强度的平方并线性刻画至本来的范围。如果本来图像中为负值，则数值平方后会重新调制为负值。

    SqureRoot：计算影像强度绝对值的平方根并线性刻画至本来的范围。如果本来图像中为负值，则数值求平方根后会重新调制为负值。

    Logarithm：计算绝对值+1的对数。并调制至本来的范围，如果原始值为负数，则计算后的数值也会调制为负数。

    Exponential：计算幂函数。并调制至本来的范围，如果原始值为负数，则计算后的数值也会调制为负数。

    Gradient：计算局部梯度。详见getGradientImage()。

    LocalBinaryPattern2D：基于切片方式（2D）计算Local Binary Pattern。

    LocalBinaryPattern3D：基于3D使用球谐函数计算Local Binary Pattern。最后返回的图像是相应的峰度图。

    了解square,squaeroot,logarithm 和exponential的数学公式，请分别参考在Imageoperations中的函数(getSquareImage(), getSquareRootImage(), getLogarithmImage(), getExponentialImage(), getGradientImage(), getLBP2DImage() 和 getLBP3DImage())。


enableImageTypes(**enabledImagetypes)

    根据自定义设置的内容，对传入的不同类型的影像分别进行设置。在此处设置的参数会覆盖kwargs中的设置。下述内容不可设置：

    - interpolator
    - resampledPixelSpacing
    - padDistance

    更新当前的设置：如果需要，激活影像（类型）。覆盖经inputImages传入的对输入影像的设置。如不采用传入的影像，使用enableInputImageByName()或disableAllInputImages()代替。

    Parameters 
    
    enabledImagetypes – 字典，key键为imagetype (original, wavelet or log)，value值为自定义设置（字典）

enableAllFeatures()

    激活所有（特征）种类和所有特征。

    Note：此函数不能激活被标记为“deprecated”的特征。可以通过使用enableFeatureByName()函方法, 或参数配置文件（在不激活所有特征的前提下通过指定特征名称）手动调用。但是在大多数情况下，结果会返回 deprecation warning。

disableAllFeatures()

    关闭所有类别。

enableFeatureClassByName(featureClass, enabled=True)

    依据给定的类别激活或关闭所有特征。

    Note：此函数不能激活被标记为“deprecated”的特征。可以通过使用enableFeatureByName()函方法, 或参数配置文件（在不激活所有特征的前提下通过指定特征名称）手动调用。但是在大多数情况下，结果会返回 deprecation warning。


enableFeaturesByName(**enabledFeatures)

    指定激活某一个特征。Key是特征类别的名字，value是特征名称组成的列表。

    如果想激活某一特征类别下的所有特征，则提供一个空列表或None作为value。enabledFeatures.keys中指定的特征种类会被更新，其中不存在的种类则会被添加进去。如果关闭整个（特征）类，可使用disableAllFeatures()或enableFeatureClassByName()代替。

### 2.4.2 Image Processing and Filters 预处理及滤波

radiomics.imageoperations.getMask(mask, **kwargs)

    获取矫正的mask。会强制矫正为像素数据类型（UInt32）。

    如果需要，同样支持提取mask中的分割（以SmipleiTK Vector 存储的image）。在这种情况下，在label_channel索引下的mask会被提取。其3D volume会作为一个标量volume输入（i.e. 其中ROI定义为label标记的对应的voxels区域）。

    最后，检查mask volume中是否包含以label标记的ROI。如果不存在label，会抛出错误（以及包含有效标签的列表）。

    Parameters

        - mask 代表mask的SimpleITK Image对象。可以是一个vector image，包含多个重叠的masks。

        - kwargs 关键词参数。关键词label_channel用于选择通道，如果没有则默认label_channel通道为0。

    Returns 

    代表mask volume的UInt32像素类型编码的SimpleITK.Image。


radiomics.imageoperations.getBinEdges(parameterValues, **kwargs)

    基于parameterValues（图像中所有分割选中voxels构成的1D array序列）计算并返回直方图。

    Fixed bin width：

    返回分组的边界，由计算得出的分组的边界值构成的列表组成，长度为N(bins)+1。两个分组的边界紧密相连，区间的左侧≤min(𝑋𝑔𝑙)。分组的边界是半开的（区间，左闭右开）。


radiomics.imageoperations.binImage(parameterMatrix,parameterMatrixCoordinates=None,**kwargs)

    使用getBinEdges()得出的binEdages离散化分布parameterMatrix（指由ROI中影像的灰度强度构成的矩阵）。只有parameterMatrixCoordinates（即影像分割）定义的voxels会被用于计算直方图并进一步离散化。影像分割以外的voxels不会变化。


radiomics.imageoperations.checkMask(imageNode, maskNode, **kwargs)

    检查mask中的ROI的大小和维度是否符合约束条件。会按以下操作进行检查。


        1. 检查mask是否与image一致（i.e. 如具有同样的大小，空间分辨率和原点）。N.B. 该项检查通过SimpleITK实施，如果失败，会记录错误，同时也会产生一个来自于SimpleITK记录的DEBUG级别的错误信息（i.e. 如果想在log记录中存储，则需将logging-level设置为debug级别）。可通过调整geometryTolerance调整容忍级别。此外，如果correctMask参数为True，PyRadiomics会检查mask内是否含有合理的ROI（在影像的物理边界内），如果存在，会对mask进行重采样至image的形状。详见Settings。

        2. 检查mask中是否有label标签。

        3. 检查ROI的维度是否＞1。（i.e. 检查ROI代表的是一个voxel(0),还是一条线（1），还是一个面（2），还是一个体积（3）），然后与所需的最少维度（由minimumROIDimensions指定）进行比较。

        4. 可选操作。检查这里是否至少有N个voxels在ROI中。N由minimumROISize定义。如果minimumROISize = None，则会跳过该检查。


    这个函数返回两个条目构成的元组。第一个条目是mask的边框。第二个条目是经过重采样矫正至输入的image影像形状的mask（如果重采样成功）。

    如果检查失败，会抛出ValueError。并且不会依据该mask提取任何特征。如果mask通过了所有测试，该函数会返回边框，会在corpToTumorMask()中使用。

    边框由第一步计算产生，并用于后续的检查。边框由SimpleITK.LabelStatisticsImageFilter()函数计算，结果为一系列索引构成的元组(L_x, U_x, L_y, U_y, L_z, U_z)。“L”“U”分别代表边框的下限和上限，“x”“y”“z”分别代表影像的三个维度。

    如果需要重复利用该处产生的边框，调用SimpleITK.LabelStatisticsImageFilter()计算，可以提高表现。

    可使用以下设置：

    minimumROIDimensions [1]: Integer，整数值，范围1-3，指定所需的最小维度（分别代表1D 2D 3D）。不包括单个voxel的分割。

    minimumROISize [None]: Integer，整数值，＞0，指定所需的voxels的最少数量。如果设置为None，则直接跳过该项检查。

    Note：如果第一项失败通常有两种情况：

        1. image和mask相匹配，但是在原点，方向或空间分辨率方面有轻微差异。确切的错误，差异还有使用的容忍程度，以DEBUG级别存储于log记录中。获取有关设置logging记录的更多信息，参阅setting up logging和helloRadiomics示例（存储于pyradiomics/examples文件夹中）。这种问题可以通过改变全局容忍程度（geometryTolerance参数）或使用强制mask矫正（correctMask参数）修正。

        2. image和mask不匹配，但是mask中确有一个ROI来代表影像中的某一存在的体积。这种情况下，需要在特征提取前进行重采样以保证image和mask之间匹配。可以通过调用correctMask()参数实现。

radiomics.imageoperations.cropToTumorMask(imageNode,maskNode,boundingBox,**kwargs)

    基于输入的label标签从影像中分割相应的区域并存储为sitkImage。

    依据影像中标记的区域创建一个sitkImage，裁切的立方体形状与标签标记的边界相符。

    Parameters

    - boundingBox 用于裁切image的边框。这是由checkMask()创建的边框。

    - label [1],label值，用于说明哪一个Image和 mask用于切割。


    Returns  经裁切的image和mask（为SimpleITK image实例）

radiomics.imageoperations.resampleImage(imageNode, maskNode, **kwargs)

    依据指定的间隔对image和mask进行重采样（默认插值方法为Bspline）。

    可以在参数配置文件中通过“interpolator”和“reampledPixelSpacing”设置激活重采样，也可以作为设置的一部分传递至特征提取器来激活。也可参阅feature extractor。

    “imageNode”和“maskNode”均为SimpleITK对象，“resampledPixelSpacing”为输出的空间分辨率。（3个元素构成的序列）

    如果仅进行平面重采样，则将平面外的维度（通常是最后的维度）的分辨率设置为0。分辨率设置为0则会使用原始的mask中的分辨率。

    仅image和labelmap的一部分会被重采样。重采样会以输入的原点进行锚定，但只有影像中ROI（即边界框定义的范围）以及padDistance覆盖的voxels会进行重采样。通过这种方式产生一个进行过重采样的，并部分经过裁切的image影像和mask掩膜。由于一些滤波会采样分割边界外的voxels，因此需要padding填充。而对于特征计算，image影像和mask影像会依据边框裁切而不进行填充，因为特征计算时不需要分割外的灰度强度值。

    重采样仅会基于输入的掩膜计算。即使image和mask具有不同的方向，但裁切下来的image和mask依然会有相同的方向（与mask的方向相同）。空间分辨率和大小由设置和ROI的边框决定。

    Note：在重采样前，未填充的ROI的边界会与边界进行比较。如果ROI的边界框超出了本来影像的物理边界，则会记录错误并返回(None, None)。同时不会提取任何特征。这会使输入的image和mask具有不同的形状，即使ROI标记了image中的一个区域。

    Note：通过调整填充padding，使只有mask内的物理空间才会被重采样。这是为了阻止image外的重采样。请注意，这里是基于image和mask具有相同物理空间的假定。如果不是，很有可能image外的voxels也会进入重采样，会被分配数值为0。因此推荐，但不是强制要求，使用和image相同大小或稍小一点的mask。


radiomics.imageoperations.normalizeImage(image, **kwargs)

    以平均值和标准差对image进行标准化操作。标准化是基于影像中所有灰度强度计算的，不仅仅是分割中的。

    𝑓(𝑥) = 𝑠(𝑥-𝜇𝑥)/𝜎𝑥

    其中

    - 𝑥和𝑓(𝑥) 分别代表原始的和标准化后的强度

    - 𝜇𝑥和𝜎𝑥代表影像中强度值的平均值和标准差。

    - s是一个由scale指定的可选调节刻度。默认情况下，设置为1。

    可以根据情况，排除异常值，即𝑥 > 𝜇𝑥 + 𝑛𝜎𝑥 or 𝑥 < 𝜇𝑥 − 𝑛𝜎𝑥。这里n大于0，并由outliers参数设定。同时这也由renmoveOutliers参数控制。异常值在图像标准化之后，使用scale之前被移除。

radiomics.imageoperations.resegmentMask(imageNode, maskNode, **kwargs)

    基于resegmentRange指定的阈值再分割mask。可以指定1个或2个阈值。在1个阈值的情况下，会保留所有等于或高于设定阈值的单位。如果这里由2个阈值，所有处于该封闭区间内的数值的voxels会被保留。（𝑇𝑙𝑜𝑤𝑒𝑟 ≤ 𝑋𝑔𝑙 ≤ 𝑇𝑢𝑝𝑝𝑒 ）。再分割的mask因此总是等于或小于原始mask。如果resegmentRange或resegmentMode包含不合理值，则会抛出ValueError。

    有3种方式可以定义阈值：
    1. absolute (default):：resegmentRange以绝对数值定义（i.e. 与image中的灰度数值一致）
    2. relative：resegmentRange以ROI中的最大数值的相对数来定义（e.g. 0.5意味着阈值为50%最大灰度值）
    3. sigma：以偏离平均值标准差sigma的数量来定义。（e.g.[-3,+3]代表偏离平均值3个标准差以内的所有数值）

radiomics.imageoperations.getOriginalImage(inputImage, inputMask, **kwargs)

    该函数不使用任何滤波，直接返回original image。该函数需要动态检查original image 是否是标准影像。

        Returns  产生original image，“orginal”和kwargs。

radiomics.imageoperations.getLoGImage(inputImage, inputMask, **kwargs)

    对输入的影像进行Laplacian of Gaussian 滤波处理，并根据指定的sigma数值分别产生派生的影像。

    Laplacian of Gaussian影像是由二次派生（Laplacian）的高斯核卷积生成的。

    用于平滑影像的高斯核定义为：

    高斯核经laplacian核∇^2𝐺(𝑥, 𝑦, 𝑧)卷积，该核对于快速变化的区域敏感，因此可以突显边界。定义高斯核的宽度的𝜎可以用来使纹理更加细腻（低𝜎）或更粗糙（高𝜎）。

    Warning：PyRadiomics中的LoG滤波是一个3D LoG滤波，因此需要3D的输入。基于单片（2D）的分割的特征也可以被提取，但是输入的影像必须是一个3D影像，并在所有维度中的最小尺寸≥𝜎。如果输入的影像太小，会记录Warning，并跳过𝜎。此外，影像的大小在每个维度内至少含有4个voxels，如果不符合该条件，不会生成LoG派生的影像。

    以下内容可以进行设置：

        sigma：浮点数值或整数值构成的列表，必须大于0。用于指定高斯核的宽度（mm）（决定凸显粗糙的程度）。

    Warning：sigma必须进行设置。如果省略，则不会计算任何LoG影像调整，并且函数会返回一个空字典。

    返回的滤波以LoG设置的名称名字：log-sigma-<sigmaValue>-3D

    参考：
    • SimpleITK Doxygen documentation
    • ITK Doxygen documentation
    • https://en.wikipedia.org/wiki/Blob_detection#The_Laplacian_of_Gaussian

        Returns  依据指定的sigma产生滤波处理后的影像，以及对应的影像类别名称和kwarg（自定义设置）。


radiomics.imageoperations.getWaveletImage(inputImage, inputMask, **kwargs)

    采用wavelet滤波处理输入的影像，产生分解值和近似值。

    可进行以下设置：

    - start_level [0]: integer，整数值，计算某一个标签时，产生的首个分解集合的0基础wavelet水平。

    - level [1]: integer，整数值，计算某一个标签时，wavelet分解水平的数量。

    - wavelet [“coif1”]: string，字符串，wavelet分解的类型。在pyWavelet.wavelist()列举了合理的取值。当前支持的取值（pywavelet version 0.4.0）（需要额外数字的，数值的范围在[]中声明）：

        – haar 
        – dmey 
        – sym[2-20] 
        – db[1-20] 
        – coif[1-5] 
        – bior[1.1, 1.3, 1.5, 2.2, 2.4, 2.6, 2.8, 3.1, 3.3, 3.5, 3.7, 3.9, 4.4, 5.5, 6.8] 
        – rbio[1.1, 1.3, 1.5, 2.2, 2.4, 2.6, 2.8, 3.1, 3.3, 3.5, 3.7, 3.9, 4.4, 5.5, 6.8] 

    返回的滤波以wavelet类型命名wavelet[level]-<decompositionName>

    N. B. 只有大于第一个层级的水平会包含到名字中。

        Returns  依据指定的sigma分别生成wavelet分解和最终近似值，以及对应的影像类型名称和kwargs(自定义设置)


radiomics.imageoperations.getSquareImage(inputImage, inputMask, **kwargs)

    计算影像强度的平方。

    结果会根据初始影像中的范围重新调整，负数值保留负数。

    𝑓(𝑥) = (𝑐𝑥)^2, 𝑐 = 1 / √︀max(|𝑥|)

    𝑥和𝑓(𝑥)分别代表原始和滤波处理后的强度。

        Returns  生成square滤波处理的影像，“square”和kwargs（自定义设置）。

radiomics.imageoperations.getSquareRootImage(inputImage, inputMask, **kwargs)

    计算影像强度绝对值的平方根。

    结果会根据初始影像中的范围重新调整，负数值保留负数。

    𝑓(𝑥) = √𝑐𝑥    𝑥≥0
          -√-𝑐𝑥   𝑥<0

    𝑐 = max(|𝑥|)

    𝑥和𝑓(𝑥)分别代表原始和滤波处理后的强度。

        Returns  生成square root滤波处理的影像，“square root”和kwargs（自定义设置）。


radiomics.imageoperations.getLogarithmImage(inputImage, inputMask, **kwargs)

    计算影像强度绝对值+1的对数。

    结果会根据初始影像中的范围重新调整，负数值保留负数。

    𝑓(𝑥) = 𝑐 log(𝑥+1)    𝑥≥0
          -𝑐 log(-𝑥+1)   𝑥<0

    𝑐 = max(|𝑥|) / log(max(|𝑥|)+1)


    𝑥和𝑓(𝑥)分别代表原始和滤波处理后的强度。

        Returns  生成logarithm滤波处理的影像，“logarithm”和kwargs（自定义设置）。

radiomics.imageoperations.getExponentialImage(inputImage, inputMask, **kwargs)

    计算影像强度的幂函数。

    结果会根据初始影像中的范围重新调整。

    𝑓(𝑥) = 𝑒^𝑐𝑥

    𝑐 = log(max(|𝑥|)) / max(|𝑥|)

    𝑥和𝑓(𝑥)分别代表原始和滤波处理后的强度。

        Returns  生成exponential滤波处理的影像，“exponential”和kwargs（自定义设置）。


radiomics.imageoperations.getGradientImage(inputImage, inputMask, **kwargs)

    计算并返回影像中的梯度水平。默认情况下，考虑影像的空间分辨率，可以通过指定gradientUseSpacing = False关闭。

    参考
        • SimpleITK documentation
        • https://en.wikipedia.org/wiki/Image_gradient

radiomics.imageoperations.getLBP2DImage(inputImage, inputMask, **kwargs)

    在2D水平计算并返回LBP。如果设置force2D为False(=从3D水平进行特征提取)，会记录一个Warning，此时滤波会以切片的方式处理影像。LBP执行的平面可以通过force2Ddimension参数来进行控制（也可参见generateAngles()）。

    可进行的设置包括（除了force2Ddimension）：

        - lbp2DRadius [1]: Float，浮点数值，＞0，用于指明采样时判定相邻单位的尺度

        - lbp2DSamples [9]: Integer，整数值，≥1，指定用于采样时样本的数量

        - lbp2DMethod [‘uniform’]: String，字符串，指定计算LBP时使用的方法

    更多内容参考scikit documentation

        Returns  生成LBP滤波影像，‘lbp-2D’和kwargs（自定义设置）

    Note：LBP经常只返回一系列很少数量的灰度层级。经常需要设置bin width。

    Warning：需要使用scikit-image软件包。如果没有，该滤波会生成Warning并且不会产生任何影像。

    参考：

    • T. Ojala, M. Pietikainen, and D. Harwood (1994), “Performance evaluation of texture measures with classification based on Kullback discrimination of distributions”, Proceedings of the 12th IAPR International Conference on Pattern Recognition (ICPR 1994), vol. 1, pp. 582 - 585.

    • T. Ojala, M. Pietikainen, and D. Harwood (1996), “A Comparative Study of Texture Measures with Classification Based on Feature Distributions”, Pattern Recognition, vol. 29, pp. 51-59.


radiomics.imageoperations.getLBP3DImage(inputImage, inputMask, **kwargs)

    使用球谐函数在3D水平计算LBP。如果force2D设置为True(=从2D水平进行特征提取)，则会记录Warning。

    仅mask中分割的voxels会被用于计算LBP。

    可进行如下设置：

        - lbp3DLevels [2]: integer，整数值，≥1，指定使用的球谐函数水平的数量 

        - lbp3DIcosphereRadius [1]: Float，浮点数值，>0，用于指明采样时判定相邻单位的尺度

        - lbp3DIcosphereSubdivision [1]: Integer，整数值，≥0，用于指定在正多面体中应用的细分部的数量。

        Returns  基于每个水平生成的LBP滤波影像，‘lbp-3D-m<level>’和kwargs（自定义设置）。以及峰度图像，‘lbp-3D-k’和kwargs。

    Note： LBP经常仅返回一个数量很少的灰度级。因此经常需要自定义设置bin width。

    Warning：需要scipy和trimesh软件包。如果没有，该滤波会生成Warning并且不会产生任何影像。

    参考：

        • Banerjee, J, Moelker, A, Niessen, W.J, & van Walsum, T.W. (2013), “3D LBP-based rotationally invariant region description.” In: Park JI., Kim J. (eds) Computer Vision - ACCV 2012 Workshops. ACCV 2012. Lecture Notes in Computer Science, vol 7728. Springer, Berlin, Heidelberg. doi:10.1007/978-3-642-37410-4_3



### 2.4.3 General Info Module 一般信息模块
class radiomics.generalinfo.GeneralInfo
Bases: object

getGeneralInfo()

    返回一个含有所有一般信息条目的字典。格式为<info_item>:<value>，并保留value的类型。对于CSV格式，若需要这些结果会转换为字符串并被引用，对于JSON格式，这些value会被解析并存储在JSON字符串中。

addStaticElements()

    添加以下信息至一般信息中：

    • Version：当前PyRadiomics的版本
    • NumpyVersion: 使用的Numpy的版本
    • SimpleITKVersion: 使用的SimpleITK的版本
    • PyWaveletVersion: 使用的PyWavelet 版本
    • PythonVersion: 在 PyRadiomics中运行的python interpreter 版本


addImageElements(image, prefix=’original’)

    计算image的缺省信息

    按下述顺序排列：

        • Hash：mask的sha1哈西值，可以在重复性检验中检查使用的是否是同一个mask。（仅在使用“original”前缀时生效）
        • Dimensionality：image中维度的数量（e.g. 2D,3D）（仅在使用“original”前缀时生效）
        • Spacing：mm级别的像素空间分辨率（x,y,z）
        • Size：以voxels数目就表示的image的维度（x,y,z）
        • mean：image中所有voxels强度的平均值。
        • Minimum: image中所有voxels强度的最小值。
        • Maxmum：image中所有voxels强度的最大值。


    添加的前缀用以说明描述是哪种image type：

        • original：载入原始image，未进行任何预处理
        • interpolated：重采样至新空间分辨率后的影像（包括裁切）


addMaskElements(image, mask, label, prefix=’original’)

    计算mask中的缺省信息

    按下述顺序排列：

        • MaskHash：mask的sha1哈西值，可以在重复性检验中检查使用的是否是同一个mask。（仅在使用“original”前缀时生效）
        • BoudingBox：用指定标签描述的ROI的边界：元素0，1，2分别代表边框底边的坐标x,y,z，元素3，4，5分别代表边框在x,y,z方向的大小。
        • VoxelNum：标签标记的ROI中voxels的数量。
        • VolumeNum：标签标记的ROI中全链接（26-connectivity）volumes的数量。
        • CenterOfMassIndex：image空间内（连续索引），ROI中心的坐标索引x,y,z
        • CenterOfMass：真实世界ROI中心坐标索引的x,y,z。
        • ROIMean：标签标记的ROI中所有voxels强度的平均值。
        • ROIMinimum：标签标记的ROI中所有voxels强度的最小值。
        • ROIMaxmum：标签标记的ROI中所有voxels强度的最大值。


    添加的前缀用以说明描述是哪种mask类型：

        • original：原始mask，未进行任何预处理。
        • corrected：经imageoperations.checkMask()校正过的mask。
        • interpolated：重采样至新空间分辨率后的mask（包括裁切）。
        • resegmented：重分割后的mask。

addGeneralSettings(settings)

    为一般设置添加字符串说明。格式是{<settings_name>:\<value>, . . . }。

addEnabledImageTypes(enabledImageTypes

    为激活的image types及任何自定义设置添加说明。格式为{<imageType_name>:{<setting_name>:\<value>, . . . }, . . . }。


### 2.4.4 Feature Class Base 特征类Base
class radiomics.base.RadiomicsFeaturesBase(inputImage, inputMask, **kwargs)

Bases: object

    这是一个抽象类，用于定义与所有特征类进行的交互。所有特征类均（直接或间接）由此继承。

    在初始化阶段，image和labelmap作为SimpleITK image对象引入（分别是inputImage和inputMask）。使用SimpleITK影像导入的原因是为了以后使用和优化SimpleITK中本来存在的特征计算器。如果没有image或mask输入，则初始化启动失败，并记录警告（但不会抛出错误）。

    Logging使用的是一个从父类“radomics”logger中继承的子类。这在生成的log记录中保留了工具箱结构。该子类logger以包含特征类别的模块命名。（e.g. “radiomics.glcm”）。

    调用特征函数之前的任何运算可以通过对_initSegmentBasedCalculation函数覆写进行添加，该函数的执行结果会作为特征提取的输入。如果需要图像离散化，可以通过在初始化中添加对_applyBinning的调用来实现，该函数还实例化保留了分组后ROI中的最大值(' Ng ')和唯一值(' GrayLevels ')的系数。该函数也将matrix变量实例化，保留了离散化的影像（imageArray变量仅保留原始灰度水平）。

    下述变量在初始化时实例化：

        • kwargs：传递至该特征类别的包含所有自定义设置的字典。
        • label：labelmap中ROI的标签值。如果不存在该关键字，则默认值为1。
        • featureNames：该特征类别中所有特征名称组成的列表。参见getFeatureNames()。
        • inputImages：代表传入的Image的SimpleITK image（维度x,y,z）。


    下列变量经_initSegmentBasedCalculation函数功能实例化：

        • inputMask：代表输入的labelmap的SimpleITK image对象（维度x,y,z）。
        • imageArray：输入的Image中的numpy arary（维度x,y,z）。
        • maskArray：numpy arrary，由布尔值构成，labelmap中等于label值的位置为True，其它地方则为False。（维度x,y,z）
        • labelledVoxelCoordinates：包括z,x,y坐标的3个numpy arrays构成的元组，分别用以标记ROI中voxels的位置。每个array的长度等于ROI中所有voxels的总的数量。
        • matrix：imageArray变量的复制，并依据指定的binWidth对ROI中的灰度值进行了离散化。该变量仅会在调用_applyBinning对特征类中_initSegmentBasedCalculation覆写时实例化。

    Note：

    尽管某些变量在此处与自定义设置具有相同的名字，但他们并不代表在特征类水平所有的设置。排列在此处的这些变量是为了帮助开发者基于这些变量开发新的特征类。了解有关更多自定义设置的信息，参见Customizing the Extraction，其中包含了有关所有设置详细的说明，包括默认值及使用的解释说明。

enableFeatureByName(featureName, enable=True)

    通过指定featureName激活或关闭某一特征。如果提供的特征不在该特征类中，会抛出lookup error，enable参数用于指定激活还是关闭特征。

enableAllFeatures()

    激活该特征类中的所有特征。

    Note：此函数不能激活被标记为“deprecated”的特征。可以通过使用enableFeatureByName()方法, 或参数配置文件（在不激活所有特征的前提下通过指定特征名称）手动调用。但是在大多数情况下，结果会返回 deprecation warning。

disableAllFeatures()

    关闭所有特征。重新设置其它任何特征。

classmethod getFeatureNames()

    动态遍历该特征分类中的所有特征。特征以get<Feature>FeatureValue标签标识，其中<Feature>是特征的名称（在分类水平上是独一无二的）。

    以字典形式返回查找到的特征的名字，其中的值为True则代表该特征已经废弃了，False代表仍在使用。({<Feature1>:<deprecated>, <Feature2>:<deprecated>, ...})。

    这个功能在初始化时调用，查找存储在featureNames变量中的所有特征。

execute()

    计算enalbedFeatures中激活的所有特征。如果在该字典中存在该特征的键，且其值为True，则该特征被激活。

    计算好的特征保存在featureValues字典中，以特征名称为key，以计算好的特征值为value。如果在计算过程中发生任何意外，会记录error，且特征值会设置为NaN。


### 2.4.5 Global Toolbox Functions
radiomics.deprecated(func)

    Decorator函数用以标记被废弃的函数。用来保证当激活所有特征时，被废弃的函数没有添加进去。

radiomics.getFeatureClasses()

    使用pkgutil遍历radiomics软件包中的所有模块，并导入该模块。

    返回一个所有包含featureClasses类的模块组成的字典，以模块名称为key，featureClass的抽象类对象为value。假定每个模块中仅有一个featureClass。

    该函数通过inspect.getmembers实现。如果一个模块中包括一个类，该类的名称以“Radiomics”起始，且继承于radiomics.base.RadiomicsFeaturesBase，则该模块会被添加至字典中。

    该迭代只会执行一次（在工具箱初始化时），接下来的调用只会返回首次调用时生成的字典。


radiomics.getImageTypes()

    返回激活的Image types构成的列表（i.e. 所有滤波影像及原始影像）。该函数通过动态匹配Imageoperations中定义的标签（get<imageType>Image）查找image types。然后返回一个包含所有可获取的Image type的名字组成的列表（<imageType>对应函数名称的一部分）。

    该迭代只会执行一次（在工具箱初始化时），接下来的调用只会返回首次调用时生成的字典。

radiomics.getParameterValidationFiles()

    返回参数配置计划的文件位置和自定义验证函数，当使用PyKwalify.core验证参数文件时需要。该函数返回一个元组，首先是计划的文件位置，其次是自定义验证函数的python脚本。

radiomics.getProgressReporter(*args, **kwargs)

    该函数返回progressReporter的实例，仅当其被设置，且logging水平设置在IFNO或DEBUG级别时有效。其它情况下返回哑进程报告器。

    为了激活进程报告，应将progessReporter变量设置为一个类对象（而不是实例），并且满足：

        1. 接收迭代并将其作为首个位置参数，以及一个关键词参数（'desc'）用以指定展示的标签

        2. 可以通过‘with’语句使用 (i.e. 具有 __enter__ 和__exit__ 功能)

        3. 可迭代(i.e. a至少指定一个__iter__函数，该函数在初始化时传递的可迭代对象上迭代).


    也可创建你自己的进程报告。为了达到该效果，额外指定一个函数_next_，具备_iter_功能返回self。__next__函数不接受参数，并返回对可迭代对象__next__函数的调用。(i.e. 返回 self.iterable.__next__())。任何结果/进程报告都可以在返回语句前插入此函数中。


radiomics.getTestCase(testCase, dataDirectory=None)

    提供测试PyRadiomics使用的image和mask。有7个测试案例可供选择：

        • brain1
        • brain2
        • breast1
        • lung1
        • lung2
        • test_wavelet_64x64x64
        • test_wavelet_37x37x37

    检查测试案例（包括一个image文件和一个mask文件，命名方式为testCase>_image.nrrd and <testCase>_label.nrrd）是否保存于dataDirectory文件夹中。如果没有，testCase会从GitHub存储库中下载（案例）并存储在dataDirectory文件夹中。如果需要也会创建dataDirectory文件夹。如果没有dataDirectory被指定，PyRadiomics会使用临时文件夹：<TEMPDIR>/pyradiomics/data

    如果测试案例被成功找到或下载，该函数会返回两个字符串：(path/to/image.nrrd, path/to/mask.nrrd)。否则返回错误（None,None）。

    Note：获取带有相应的单个切片标签的测试案例，添加“_2D”至testCase。

radiomics.setVerbosity(level)

    改变PyRadiomics在提取时输出的信息量。设置级别越低，输出的信息越多(stderr)。

    使用level（Python定义的logging 级别）参数，下述级别可以使用：
        
        60：安静模式，不会输出任何信息至stderr。
        50：仅记录并输出“CRITICAL”级别的信息。
        40：记录并打印“ERROR”级别及以上的信息。
        30：记录并打印“WARNING”级别及以上的信息。
        20：记录并打印“INFO”级别及以上的信息
        10：记录并打印“DEBUG”级别及以上的信息（i.e.即所有log信息）

    默认情况下，radiomics logger设置级别为“INFO”，stderr handler设置级别为“WARNING”。 因此，通过向radiomics记录器添加适当的处理程序，可以轻松地设置存储“INFO”级别及以上的记录，而stderr的输出仍然只包含warnings和errors。

    Note：此函数假定在工具箱初始化时添加到radiomics记录器的处理程序没有从记录器处理程序中删除，因此仍然是第一个处理程序。

    Note：这不会影响logger本身的记录级别（e.g.如果verbose level = 3，且向记录器添加了适当的处理程序，并且记录器的记录级别设置为正确的级别，则具有DEBUG级别的记录消息仍然可以存储在记录文件中。例外：在verbosity 的级别设置为DEBUG时，logger 的级别也会低于DEBUG。如果提升verbosity的级别，logger的级别会维持在DEBUG。）

## 2.5 Radiomic Features 影像组学特征

该部分包括所有通过PyRadiomics可提取的特征的定义。并按照下列顺序排列：

+ First Order Statistics (19 features)

+ Shape-based (3D) (16 features)

+ Shape-based (2D) (10 features)

+ Gray Level Cooccurence Matrix (24 features)

+ Gray Level Run Length Matrix (16 features)

+ Gray Level Size Zone Matrix (16 features)

+ Neighbouring Gray Tone Difference Matrix (5 features)

+ Gray Level Dependence Matrix (14 features)

所有特征种类，除了shape特征可基于源影像或派生影像进行计算外，其余仅由基于滤波处理的影像获得。Shape特征计算不基于（影像中的）灰度水平，基于作为标记的掩膜进行计算。如果激活，会根据传入的多种image types单独计算影像特征，并在结果中列出，就像在原始图像上计算一样。

下述大多数特征的定义与IBSI中的定义相一致，可以参考Zwanenburg等人的文章。在不同的地方，以笔记形式说明了不同。

### 2.5.1 First Order Features

class radiomics.firstorder.RadiomicsFirstOrder(inputImage, inputMask, **kwargs
)

Bases: radiomics.base.RadiomicsFeaturesBase

    First-order特征用以描述，在通用和基本尺度上，mask标记的影像区域中体素强度的分布情况。

    定义：

        X 代表ROI中𝑁𝑝个体素的集合

        P(𝑖) 是带有𝑁𝑔 个离散强度分级的一阶直方图，𝑁𝑔 代表非零分组的数目，等于使用参数binWidth参数定义的width从0开始划分的数目。

        𝑝(𝑖)是标准化的一阶直方图，等于P(𝑖)/𝑁𝑝

    可设置内容如下：

        voxelArrayShift [0]: Integer，整数值，计算Energy， Total Energy 和RMS时，这个数值会在灰度强度上添加以避免负数。如果使用CT影像，或数值没有经过平均数0标准化，建议将该参数设置为固定的数值（e.g. 2000），这可以确保在影像中没有负数。请牢记，该数值越大，体积混杂效应影响越大。

    Note：在IBSI特征定义中，并没有对零下的灰度进行矫正，如果想达到同样的效果，设置voxelArrayShift为0。

getEnergyFeatureValue()

    1.  Energy

    这里，𝑐是一个可选参数，由voxelArrayShift设定，以整体平移影像中的强度以避免负数值出现在X中，以确保最低的灰度值也对Energy有贡献，并代替灰度值接近0的体素。

    Energy是一个影像中体素强度的度量，越大的数值产生的平方和会越大。
    
    Note：该特征受体积混淆影响，c值越大造成的体积混淆影响越大。


getTotalEnergyFeatureValue()

    2.  Total Energy

    这里，c是一个可选参数，由voxelArrayShift设定，以整体平移影像中的强度以避免负数值出现在X中，以确保最低的灰度值也对Energy有贡献，并代替灰度值接近0的体素。

    Total Energy是在立方mm尺度衡量的Energy特征。

    Note：该特征受体积混淆影响，c值越大造成的体积混淆影响越大。

    Note：IBSI中不包含该特征。


getEntropyFeatureValue()

    3. Entropy

    𝜖是任一小正数(≈ 2.2 × 10−16)。

    Entropy用以描述影像中数值（即强度）的不确定性/随机状态。衡量了用以编码影像中数值的所需信息的平均数量。

    Note：在IBSI中以Intensity Histogram Entropy定义。


getMinimumFeatureValue()

    4. Minimum

    minimum = min(X)

get10PercentileFeatureValue()

    5. 10th percentile

    10分位数。

get90PercentileFeatureValue()

    6. 90th percentile

    90分位数。

getMaximumFeatureValue()

    7. Maximum

    maximum = max(X)

    ROI中的最大灰度值。


getMeanFeatureValue()

    8. Mean

    ROI中的平均灰度值。


getMedianFeatureValue()

    9. Median

    ROI中灰度强度的中位数。


getInterquartileRangeFeatureValue()

    10. Interquartile Range

    interquartile range = P75 − P25

    四分位间距。


getRangeFeatureValue()

    11. Range

    ROI中灰度值的范围


getMeanAbsoluteDeviationFeatureValue()

    12. Mean Absolute Deviation (MAD)

    平均绝对偏差，即所有数值与平均值绝对距离之差的平均值。


getRobustMeanAbsoluteDeviationFeatureValue()

    13. Robust Mean Absolute Deviation (rMAD)

    粗平均绝对偏差，同上，但是只统计10分位至90分位的数值。


getRootMeanSquaredFeatureValue()

    14. Root Mean Squared (RMS)

    这里，𝑐 是一个可选参数，由voxelArrayShift设定，以整体平移影像中的强度以避免负数值出现在X中，以确保最低的灰度值也对RMS有贡献，并代替灰度值接近0的体素。

    Energy是一个影像中体素强度的度量，越大的数值产生的平方和会越大。

    RMS是强度平方平均值的平方根。是另一种影像强度的测度。该特征受体积混淆影响，c值越大造成的体积混淆影响越大.

getStandardDeviationFeatureValue()

    15. Standard Deviation

    标准差。

    Note：因为该特征与方差有关，所以默认不提取该特征。如果想提取该特征，可通过单独指定名称来实施。（i.e.如果不通过指定单一的特征，则不会提取该特征（如同时激活“所有”特征），但是可以通过指定某一特征的方式激活）。IBSI中不包含该特征的定义（与方差相关）。

getSkewnessFeatureValue()
    16. Skewness

    𝜇3是三阶中心距。

    Skewness用来测量所有数值关于平均值的不对称分布情况。基于峰尾延伸和数据峰度集中的情况（译者注：可参考分布直方图中，数据集中的峰的情况及两侧延伸的尾的概念），这个数值可以是正数也可以是负数。

    相关链接：
    https://en.wikipedia.org/wiki/Skewness

    Note：在扁平的情况下，标准差和四阶中心距都会是0。在这种情况下，返回结果为0。


getKurtosisFeatureValue()
    17. Kurtosis

    𝜇4是四阶中心矩。

    Kurtosis用以评估ROI中数值分布“陡峭”程度。Kurtosis值越大，说明数据越向两侧分布，而不是集中分布，值越小，则说明情况恰相反：数据更集中于平均值。

    相关链接: https://en.wikipedia.org/wiki/Kurtosis

    Note：在扁平的情况下，标准差和四阶中心距都会是0。在这种情况下，返回结果为0。

    Note：IBSI的定义不止于kurtosis，其kurtosis经-3矫正，正太分布情况下结果为0。PyRadiomics中的kurtosis未经过校正长生的结果比IBSI的结果大3。


getVarianceFeatureValue()

    18. Variance

    方差。

getUniformityFeatureValue()
    19.  Uniformity

    Uniformity是各强度的平方和。用以测量image array的均匀性，Uniformity越大代表均匀性越高或强度分布范围越小。

    Note：IBSI定义为Intensity Histogram Uniformity。


### 2.5.2 Shape Features (3D)
class radiomics.shape.RadiomicsShape(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase

    在这个分类下，我们描述了ROI在三维水平的大小和形态。这些特征不依赖于ROI中的灰度强度分布，仅基于非派生的image和mask计算。

    除非特别声明，基于近似的三角形网格划分计算特征。为了建立这个网格划分，顶点定义为介于ROI中的一个体素与ROI外的一个体素边缘上中间的点。通过链接这些顶点，形成一个三角形网格划分，每个三角形由三个相连的点构成，并与另一个三角形共享每条边。

    该网格划分是通过移动立方体算法生成。在这个算法中，（想象）一个2*2的立方体在mask空间内移动。在每一点，立方体的角被标记为“segmented”（1）或“not segmented”（0）。使用二进制编码标记这些“角”，得到一个独一无二的立方体索引（0-255）。这些索引用于鉴别哪些三角出现在立方体中，可在查阅表中查阅。

    通过这种方式获得的这些三角形网格划分，法向量(由描述3条边中的2条的向量的叉乘得到)具有相同的方向。在PyRadiomics，这些计算后得到的法线均指向外侧。这对于计算MeshVolume时获取正确的标记的volume是必须的。

    在此处：

        • 𝑁𝑣代表ROI中voxels的数量

        • 𝑁𝑓 代表网格划分三角形的数量

        • 𝑉 网格划分的体积，单位mm3，通过getMeshVolumeFeatureValue()计算获得

        • 𝐴 网格划分的面积，单位mm2，通过getMeshSurfaceAreaFeatureValue()计算获得

    参考
        Lorensen WE, Cline HE. Marching cubes: A high resolution 3D surface construction algorithm. ACM SIGGRAPH Comput Graph Internet. 1987;21:163-9.


getMeshVolumeFeatureValue()

    1. Mesh Volume

    ROI的体积V的计算是通过计算ROI中三角形网格划分得来。对于网格划分中每一个面i，由三个点a,b,c构成，每个由该面和Image的原点O构成一个四面体，计算可得其体积Vf。公式（1）中体积的符号由法线的符号决定，因此必须统一指向ROI内或外。

    然后通过公式（2）计算所有Vi之和，得到ROI的总体积。

    Note：了解更多如何使用网格划分计算体积的文档，参考IBSI的文档，该特征定义为Volume。

getVoxelVolumeFeatureValue()

    2.  Voxel Volume

    ROI体积Vvoxel近似等于ROI中体素的数量与单个体素体积Vk相乘的结果。这是一个不够精确的体积，并不会用于其它特征计算。该特征不是经过网格划分计算得到，也不会用于其它shape features计算。

    Note：在IBSI中定义为Approximate Volume。


getSurfaceAreaFeatureValue()
    3.  Surface Area

    其中：

    ai bi和ai ci是网格划分中第ith个三角形的两条边，由定点ai, bi, ci构成。

    为了计算表面积，首先计算网格划分中每个三角形的表面积ai（1）。然后计算这些表面积之和得到总面积（2）。

    Note：在IBSI中定义为Surface Area。

getSurfaceVolumeRatioFeatureValue() 

    4.  Surface Area to Volume ratio

    值越小，说明体积压缩越明显（球形），该特征是无量纲度量，并且（部分）与ROI的体积相关。


getSphericityFeatureValue()

    5.  Sphericity

    Sphercity是标记区域内形状相对于球形的测度。他是一个无量纲测度，与刻度和方向无关。取值范围0 < 𝑠𝑝ℎ𝑒𝑟𝑖𝑐𝑖𝑡𝑦 ≤ 1，1代表是个完美的球形（相对于其它形状，在给定的体积下，具有最小的表面积。）

        Note：该特征与Compactness 1, Compactness 2 和 Spherical Disproportion相关。在pyradiomics/examples/exampleSettings提供的默认参数配置文件中，Compactness 1 and Compactness 2没有被激活。


getCompactness1FeatureValue()

    6.  Compactness 1

    与Sphericity相似，Compactness 1 也是包块面积相对于球形（最紧实）的测度。因此他与Sphericity相关且是富余的。在这里提供是为了特征的完整性。取值介于0 < 𝑐𝑜𝑚𝑝𝑎𝑐𝑡𝑛𝑒𝑠𝑠 1 ≤ 1/6𝜋之间，1/6𝜋代表是个完美的球形。

    根据定义，

    Note：该特征与Compactness 1, Compactness 2 和Spherical Disproportion相关。因此，这个特征被标记下来，默认情况下不激活。（i.e.这个特征不可通过非指定的方式激活（激活“所有”特征），但是可以通过指定单个特征的方式激活）。如果想在提取中提取该特征，可以通过指定名称的方式激活该特征提取。


getCompactness2FeatureValue()

    7.  Compactness 2

    与Sphericity和Compactness 1相似，Compactness 2 也是包块面积相对于球形（最紧实）的测度。他是一个无量纲测度，与刻度和方向无关。。取值介于0 < 𝑐𝑜𝑚𝑝𝑎𝑐t𝑛𝑒𝑠𝑠 2 ≤ 1之间，1代表是个完美的球形。

    根据定义，

    Note：该特征与Compactness 1, Shpericity 和Spherical Disproportion相关。因此，这个特征被标记下来，默认情况下不激活。（i.e.这个特征不可通过非指定的方式激活（激活“所有”特征），但是可以通过指定单个特征的方式激活）。如果想在提取中提取该特征，可以通过指定名称的方式激活该特征提取。


getSphericalDisproportionFeatureValue()

    8.  Spherical Disproportion

    R是具有相同体积的球形的半径，等于

    Spherical Disproportion是包块表面积与具有相同体积的球形肿块的面积的比值，是Sphericity的倒数。至此取值范围为大于等于1，1代表是个完美的球形。

    Note：该特征与Compactness 1, Shpericity 和Spherical Disproportion相关。因此，这个特征被标记下来，默认情况下不激活。（i.e.这个特征不可通过非指定的方式激活（激活“所有”特征），但是可以通过指定单个特征的方式激活）。如果想在提取中提取该特征，可以通过指定名称的方式激活该特征提取。

getMaximum3DDiameterFeatureValue()

    9.  Maximum 3D diameter

    Maximum 3D diameter定义为包块表面网格两个顶点之间最大的欧几里得距离。

    另一个名称是Feret Diameter。

getMaximum2DDiameterSliceFeatureValue()

    10. Maximum 2D diameter (Slice)

    Maximum 2D diameter (Slice)定义为在row-column平面上（通常为横轴面），包块表面网格两个顶点之间最大的欧几里得距离。


getMaximum2DDiameterColumnFeatureValue()

    11. Maximum 2D diameter (Column)

    Maximum 2D diameter (Column) 定义为在row-slice平面上（通常为冠状面），包块表面网格两个顶点之间最大的欧几里得距离。

getMaximum2DDiameterRowFeatureValue()

    12. Maximum 2D diameter (Row)

    Maximum 2D diameter (Row) 定义为在column-slice平面上（通常为矢状面），包块表面网格两个顶点之间最大的欧几里得距离。

getMajorAxisLengthFeatureValue()

    13. Major Axis Length

    计算ROI构成的椭球体最大长径，使用最大主成分𝜆𝑚𝑎𝑗𝑜𝑟计算。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

getMinorAxisLengthFeatureValue()

    14. Minor Axis Length

    计算ROI构成的椭球体第二长径，使用最大主成分𝜆𝑚inor计算。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

getLeastAxisLengthFeatureValue()

    15. Least Axis Length

    计算ROI构成的椭球体最小轴长，使用最大主成分𝜆least计算。在2的分割中，数值为0.

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

getElongationFeatureValue()

    16. Elongation

    Elongation用于描述ROI形状中最大和第二两个主成分之间的关系。因计算的原因，此处公式定义为真正elongation的倒数。

    𝜆major和𝜆minor是最大和第二长主成分轴。取值介于1（第一、第二主成分交叉的部分更贴近于球形，没有延长）和0（最大程度的延长了：i.e.一个一维的长线）。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

getFlatnessFeatureValue()

    17. Flatness

    Flatness用于描述ROI形状中最大和最小两个主成分之间的关系。因计算的原因，此处公式定义为真正flatness的倒数。

    𝜆major和𝜆least是最大和最小长主成分轴。取值介于1（第一、第二主成分交叉的部分更贴近于球形，没有延长）和0（最大程度的延长了：i.e.一个一维的长线）。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

### 2.5.3 Shape Features (2D)
class radiomics.shape2D.RadiomicsShape2D(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase

    在这一组特征中，我们计算ROI二维尺度上的大小和形态。这些特征不依赖于ROI中的灰度强度分布，仅基于非派生的image和mask计算。

    除非特别声明，基于近似的圆形网格划分计算特征。为了建立这个网格划分，顶点定义为介于ROI中的一个体素与ROI外的一个体素边缘上中间的点。通过链接这些顶点，得到由这些连线构成的网格，每条线由两个相连的点构成，并与另外一条线共享每个点。

    这个网格划分经优化后的移动立方体算法生成。在该算法中，一个2*2的方块在mask空间移动（2D）。在每个位置，方块的角被标记为“segmeted”（1）和“not segmented”（2）。使用二进制编码标记这些“角”，得到一个独一无二的方块索引（0-255）。这些索引用于鉴别哪些线出现在方块中，可在查阅表中查阅。

    通过这种方式定义这些线，由这些点构成的三角形的法线及其原点都指向同一个方向。通过这种方式标记的三角形表面积，在计算总和时，正面积表示的是ROI内部的面积，负数值表示的是ROI外部的面积，会被去除。

    使：
        • 𝑁𝑣代表ROI中pixels的数量 
        • 𝑁𝑓代表圆周网格划分线的数量 
        • 𝑉 网格划分的表面积，单位mm2，通过getMeshSurfaceFeatureValue()计算获得 
        • 𝐴 网格划分的周长，单位mm，通过getPerimeterFeatureValue()计算获得


    Note：这个分类进可以用于2D masks的计算。为了确保正确的进程，需设置force2d为True，并设置force2Ddimension关闭平面外的维度（e.g. 对于横轴面为0（即z轴））。最后，具有1个维度。如果设置不正确，最后会产生ValueError.

    参考
    • Lorensen WE, Cline HE. Marching cubes: A high resolution 3D surface construction algorithm. ACMSIGGRAPH Comput Graph Internet. 1987;21:163-9.


getMeshSurfaceFeatureValue()

    1.  Mesh Surface

    O𝑖 a𝑖 和O𝑖 b𝑖 是网格划分中的第i个三角形，由a𝑖，bi，和顶O围成。

    为了计算表面积，首先计算每个网格划分中每个三角的表面积𝐴𝑖 （1）。然后计算所有表面积之和，得到总表面积（2）。计算面积中的正负号，会却将ROI外的面积从总面积中扣除。


getPixelSurfaceFeatureValue()

    2.  Pixel Surface

    ROI的表面积𝐴𝑝𝑖𝑥𝑒𝑙近似等于ROI中像素的数量乘以单个像素𝐴𝑘的面积。这是一个表面积的近似估计。该特征不是经过网格划分计算得到也不会用于其它2D shape features计算。

getPerimeterFeatureValue()

    3. Perimeter

    a𝑖 b𝑖是网格划分中第i条线段的顶点。

    为了计算周长，首先计算网格划分中每条线段的周长𝐴𝑖（1）。然后计算总和。


getPerimeterSurfaceRatioFeatureValue()

    4. Perimeter to Surface ratio

    越低的值表明越接近圆形。该特征无量纲，（部分）与ROI表面相关。


getSphericityFeatureValue()

    5. Sphericity

    R代表与ROI相同的圆的半径，等于

    Sphericity是包块区域的周长与具有相同面积的圆的周长的比例，测度肿块形状与圆的相似性。该特征是一个无量纲度量，与刻度和位置无关。取值范围0 < 𝑠𝑝ℎ𝑒𝑟𝑖𝑐𝑖𝑡𝑦 ≤ 1，1代表是个完美的圆形（与其它形状相比圆具有给定面积下最小周长）。

    Note: 该特征与Spherical Disproportion相关。因此默认情况下仅提取该特征。


getSphericalDisproportionFeatureValue()

    6.  Spherical Disproportion

    Spherical Disproportion是包块周长与具有相同面积的球形肿块的周长的比值，是Sphericity的倒数。至此取值范围为大于等于1，1代表是个完美的球形。

    Note：该特征与Shpericity相关。因此，这个特征被标记下来，默认情况下不激活。（i.e.这个特征不可通过非指定的方式激活（激活“所有”特征），但是可以通过指定单个特征的方式激活）。如果想在提取中提取该特征，可以通过指定名称的方式激活该特征提取。


getMaximumDiameterFeatureValue()

    7. Maximum 2D diameter

    Maximum 2D diameter (Slice)定义为在包块表面网格划分上两个顶点之间最大的欧几里得距离。

getMajorAxisLengthFeatureValue()

    8. Major Axis Length

    计算ROI构成的椭球体最大长径，使用最大主成分𝜆𝑚𝑎𝑗𝑜𝑟计算。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

getMinorAxisLengthFeatureValue()

    9. Minor Axis Length

    计算ROI构成的椭球体第二长径，使用最大主成分𝜆𝑚inor计算。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。

getElongationFeatureValue()

    10. Elongation

    Elongation用于描述ROI形状中最大和第二两个主成分之间的关系。因计算的原因，此处公式定义为真正elongation的倒数。

    𝜆major和𝜆minor是最大和第二长主成分轴。取值介于1（第一、第二主成分交叉的部分更贴近于球形，没有延长）和0（最大程度的延长了：i.e.一个一维的长线）。

    主成分分析是基于ROI中心的物理位置坐标分析而成。因此在计算时考虑了空间分辨率的影响，但并没有用到网格划分。


### 2.5.4 Gray Level Co-occurrence Matrix (GLCM) Features
class radiomics.glcm.RadiomicsGLCM(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase

    灰度共生矩阵是一个大小为𝑁𝑔 × 𝑁𝑔 的矩阵P(𝑖, 𝑗|𝛿, 𝜃)，用以描述mask标记的影像区域内的二阶联合的概率。该矩阵中第I行J列的元素，代表具有相应的信号强度的两个像素组合对出现在影像中的数量，该两个像素之间延𝜃角度相距𝛿个像素。与中心体素相聚的距离𝛿参考无穷范数标准。对于距离=1，在3D模型中共有13个角度指向总计26个相连的邻域，对于距离=2则共有98个（共计49个角度）。


    Note，在pyradiomics中默认计算对称GLCM！


    以一个二维案例举例，下述矩阵i代表一个5*5大小的影像，灰度强度分级为5：


    设定距离为1（即共生的两点相距1个像素），角度为0（即平行方向，i.e 对于某一体素可向左或向右），可得到对称GLCM

    其中：
        𝜖代表任一小的正数(≈ 2.2 × 10−16)
        P(𝑖, 𝑗)是关于任意距离𝛿 和角度𝜃的共生矩阵
        𝑝(𝑖, 𝑗)是标准化的共生矩阵等于
        𝑁𝑔是影像中灰度强度的分级
        𝑝𝑥(𝑖)是行边缘概率
        𝑝𝑦(𝑗)是列边缘概率
        𝜇𝑥是𝑝𝑥平均值
        𝜇𝑥是𝑝𝑦的平均值
        𝜎𝑥是𝑝𝑥的标准差
        𝜎𝑥是𝑝𝑦的标准差
        𝐻𝑋是𝑝𝑥的熵值
        𝐻𝑌是𝑝𝑦的熵值
        𝐻𝑋𝑌是𝑝(𝑖, 𝑗)的熵值


    默认情况下，特征值是基于不同角度的GLCM计算的，之后返回这些值的平均值。如果激活了的距离权重设置，则GLCM会根据权重因子W设定，然后再进行加总和标准化。特征会根据以上结果进行计算。权重因子W会基于两体素间距离计算，公式为𝑊 = 𝑒^（−‖𝑑‖^2），d代表在相应角度中依据’weightingNorm’设置的距离。


    可进行下述自定义设置。

        distances [[1]]: List of integers，整数值构成的列表。用于衡量沿某一角度，中心voxel及其相邻voxel间的距离。

        symmetricalGLCM [True]: boolean，布尔值，用以说明共生对是否在相应角度中沿两个方向上寻找，其结果为对于i和j具有相同的分布的对称矩阵。参考Haralick等人定义的GLCM对阵矩阵。

        weightingNorm [None]: string，字符串，指定在衡量距离时使用的标准。可参考的设置如下。

        – ‘manhattan’: 一阶范数 
        – ‘euclidean’: 二阶范数 
        – ‘infinity’: 无穷范数 
        – ‘no_weighting’: GLCMs采用因子1权重并求和 
        – None: 不采用权重，返回基于单独的矩阵计算的平均值

    对于提供的其它数值，会记录warning，同时会采用“no_weighting”权重。

    参考
    • Haralick, R., Shanmugan, K., Dinstein, I; Textural features for image classification; IEEE Transactions on Systems, Man and Cybernetics; 1973(3), p610-621
    • https://en.wikipedia.org/wiki/Co-occurrence_matrix
    • http://www.fp.ucalgary.ca/mhallbey/the_glcm.htm



getAutocorrelationFeatureValue()

    1. Autocorrelation

    Autocorrelation是纹理细腻和粗糙程度的度量。


getJointAverageFeatureValue()

    2. Joint Average

    返回i分布的平均灰度强度。

    Warning：此公式表示的是i分布的平均数，和j的分布无关。因此，仅在GLCM是对称生成的时候有效，此时𝑝𝑥(𝑖) = 𝑝𝑦(𝑗), 𝑖 = 𝑗。


getClusterProminenceFeatureValue()

    3. Cluster Prominence

    Cluster Prominence是关于GLCM偏态和不对称程度的测量。越大的数值表明越偏离平均值，越低的数值表明数据越靠近平均值，意味着变异越少。


getClusterShadeFeatureValue()

    4. Cluster Shade

    Cluster Shade是GLCM矩阵偏态和均匀性的测量。越高的值表明越偏离平均值。


getClusterTendencyFeatureValue()

    5. Cluster Tendency

    Cluster Tendency是具有相同灰度分级体素分组的测量。
　　

getContrastFeatureValue()

    6. Contrast

    Contrast是局部强度变异的测量，侧重于（GLCM矩阵中）非对角线上的数值 (𝑖 = 𝑗)。越大的值表明相邻体素间强度差异越大。


getCorrelationFeatureValue()

    7. Correlation

    Correlation是介于0与1之间的值，衡量GLCM中灰度值与各自体素的线性相关性。

    Note：当ROI（扁平的区域）中仅有一个灰度分级时，𝜎𝑥和𝜎y为0。在这种情况下，结果会返回1，这是基于单一角度评估的。


getDifferenceAverageFeatureValue()

    8. Difference Average

    Difference Average衡量了灰度值相同的共生对与灰度值不同值的共生对出现之间的关系。


getDifferenceEntropyFeatureValue()

    9. Difference Entropy

    Difference Entropy是邻域强度差异的随机性/变异性的度量。


getDifferenceVarianceFeatureValue()

    10. Difference Variance

    Difference Variance是对偏离平均值的非同值强度对使用更高的权重得到的有关异质性的测量。

getDissimilarityFeatureValue()

    DEPRECATED. Dissimilarity

    Warning：该特征已经被废弃了，因为数学上等于Difference Average  getIdFeatureValue()。激活此特征会记录一个Deprecation-Warning（不会打断其它特征的提取），不会为此特征计算任何值。


getJointEnergyFeatureValue()

    11. Joint Energy

    Energy是图像中均匀模式的测量。值越大，意味着在影像中存在更多的强度值对在更高的频次上彼此相邻。

    Note：在IBSI中定义为Angular Second Moment。


getJointEntropyFeatureValue()

    12.  Joint Entropy

    Joint entropy是邻域强度值随机/变异程度的度量。

    Note：在IBSI中定义为Joint entropy。


getHomogeneity1FeatureValue()

    DEPRECATED. Homogeneity 1

    Warning：该特征已经被废弃了，因为数学上等于Inverse Difference  getIdFeatureValue()。激活此特征会记录一个Deprecation-Warning（不会打断其它特征的提取），不会为此特征计算任何值。

getHomogeneity2FeatureValue()

    DEPRECATED. Homogeneity 2

    Warning：该特征已经被废弃了，因为数学上等于Inverse Difference Moment getIdFeatureValue()。激活此特征会记录一个Deprecation-Warning（不会打断其它特征的提取），不会为此特征计算任何值。


getImc1FeatureValue()

    13. Informational Measure of Correlation (IMC) 1

    IMC1评估了i和j概率分布之间的相关性（定量纹理的复杂程度），使用互用信息I(x, y)。

    然而，在这个公式中，分子定义为HXY - HXY1 (i.e. −𝐼(𝑥, 𝑦))，因此≤0。这反应了在原始haralick的文章中是如何定义该特征的。

    在分布是独立的情况下，没有交互信息，结果为0。在完全相关的一致分布的情况下，互用信息等于log2(𝑁𝑔)。

    最后，HXY-HXY1除以两个边缘熵的最大值，在完全相关的情况下（不一定是一致的；低复杂程度），会导致MC1=-1，HX = HY = 𝐼(𝑖, 𝑗)。

    Note：在HX和HY均为0的情况下（就像在一个平的区域中），会返回任意值0以避免除以0。这是根据单一角度计算完成的。（i.e. 在平均之前）。


getImc2FeatureValue()

    14.  Informational Measure of Correlation (IMC) 2

    IMC2同样用于评估i和j概率分布之间的相关性（定量纹理的复杂程度）。

    需注意的是，HXY1=HXY2，以及HXY2-HXY≥0意味着2个分布的互信息。因此，IMC2=\[0,1），0代表2个分布独立（没有互信息）的情况，最大值则代表两个互相依赖、一致的分布的情况（最大互信息，等于log2(𝑁𝑔)）。在后一种情况中，最大值等于√︀1 − 𝑒…^(−2 log2(𝑁𝑔))，接近为1。

    Note：由于机器精度误差，有可能出现HXY＞HXY2，有可能导致结果为复数。这种情况下，IMC2结果会返回为0。这是根据单一角度计算完成的。（i.e. 在平均之前）。


getIdmFeatureValue()

    15.  Inverse Difference Moment (IDM)
    
    IDM (a.k.a Homogeneity 2)是image中局部同质性的测量。IDM权重是Contrast 权重的倒数（在GLCM的对角线i=j中呈指数递减）。


getMCCFeatureValue()

    16.  Maximal Correlation Coefficient (MCC)

    Maximal Correlation Coefficient是纹理复杂程度的测量，且0≤MCC≤1。

    在区域平坦的情况下，每一个GLCM矩阵形状为（1，1），仅产生一个特征值。在这种情况下，会返回结果1。


getIdmnFeatureValue()

    17. Inverse Difference Moment Normalized (IDMN)

    IDMN是image中局部同质性的测量。IDMN权重是Contrast权重的倒数（在GLCM中延对角线i=j指数递减）。不同于Homogeneity2，IDMN通过除以离散强度值总数的平方，将强度值之差的平方归一化。


getIdFeatureValue()

    18. Inverse Difference (ID)

    ID是image中局部同质性的另一种度量方法。灰度水平越一致，分母水平越低，结果越大。


getIdnFeatureValue()

    19.  Inverse Difference Normalized (IDN)

    IDN是局部同质性的另一种度量方法。不同于Homogeneity1，IDN通过除以离散强度值总数将邻域强度值之差归一化。


getInverseVarianceFeatureValue()

    20.  Inverse Variance

    Note，K=0时会跳过，因为这会使结果除以0。


getMaximumProbabilityFeatureValue()

    21.  Maximum Probability

    Maximum Probability是最多的邻域强度对出现的概率。

    Note：在IBSI中定义为Joint maximum。

getSumAverageFeatureValue()

    22.  Sum Average

    Sum Average测量了低强度对出现和高强度对出现的关系。

    Warning：GLCM是对称矩阵时，x=y，因此Sum Average = 𝜇𝑥 + 𝜇𝑦 = 2𝜇𝑥 = 2 * 𝐽𝑜𝑖𝑛𝑡𝐴𝑣𝑒𝑟𝑎𝑔𝑒。参见这里的公式（4）（5）（6）以证明Sum Average =𝜇𝑥 +𝜇𝑦。在examples/exampleSettings文件夹中提供的参数配置文件中，该特征被关闭了。


getSumVarianceFeatureValue()

    DEPRECATED. Sum Variance

    Warning：这个特征已经被废弃了，因为其在数学上等于Cluster Tendency getClusterTendencyFeatureValue()。参见此处以查看证明过程。激活此特征会记录一个Deprecation-Warning（不会打断其它特征的提取），不会为此特征计算任何值。


getSumEntropyFeatureValue()

    23.  Sum Entropy

    Sum Entropy是邻域强度差异之和。


getSumSquaresFeatureValue()

    24.  Sum of Squares
    
    Sum of Squares or Variance是GLCM中邻域强度对关于平均强度水平分布情况的测度。

    Warning：此公式表示的是i分布的平均数，和j的分布无关。因此，仅在GLCM是对称生成的时候有效，此时𝑝𝑥(𝑖) = 𝑝𝑦(𝑗), 𝑖 = 𝑗。

    Note：在IBISI中定以为Joint Variance。


### 2.5.5 Gray Level Size Zone Matrix (GLSZM) Features

class radiomics.glszm.RadiomicsGLSZM(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase


    Gray Level Size Zone (GLSZM)用于定量image中的灰度强度区域。灰度区域定义为一片具有相同灰度强度的区域。相互相连的体素定义为，依据无穷范数尺度，与其相隔1个距离的体素（在3D水平上有26个相连的区域，在2D水平上有8个相连的区域）。在一个GLSZM矩阵𝑃(𝑖, 𝑗)中，第i行j列的元素代表在相应的影像中，灰度强度为i的，相连区域大小为j的区域的数量。与GLCM和GLRLM相比，GLSZM与旋转无关，在ROI所有方向上只计算一个矩阵。

    以一个二维案例示例，如下所示的5*5大小的Image中，具有5个分离等级水平的灰度强度：

    则GLSZM矩阵为：

    其中：
        𝑁𝑔是图像中离散强度值的数目
        𝑁𝑠是图像中离散区域大小的数量
        𝑁𝑝是图像中体素的数目
        𝑁𝑧是ROI中区域的数目，等于
        P(𝑖, 𝑗)是区域大小矩阵
        p(𝑖, 𝑗)是标准化的区域大小矩阵，等于

        Note：定义GLSZM特征的公式，与GLRLM中提取的特征公式一致。

    参考
    • Guillaume Thibault; Bernard Fertil; Claire Navarro; Sandrine Pereira; Pierre Cau; Nicolas Levy; Jean Sequeira; Jean-Luc Mari (2009). “Texture Indexes and Gray Level Size Zone Matrix. Application to Cell Nuclei Classification”. Pattern Recognition and Information Processing (PRIP): 140-145.
    • https://en.wikipedia.org/wiki/Gray_level_size_zone_matrix

getSmallAreaEmphasisFeatureValue()

    1. Small Area Emphasis (SAE) 

    SAE是一种小区域分布的度量方式，值越大，代表小的区域数目越多，纹理越细致。


getLargeAreaEmphasisFeatureValue()

    2.  Large Area Emphasis (LAE)

    LAE是一种大区域分布的度量方式，值越大，代表大的区域数目越多，纹理越粗糙。


getGrayLevelNonUniformityFeatureValue()

    3.  Gray Level Non-Uniformity (GLN)

    GLN衡量影像中灰度强度的变异程度，值越低表明图像中同质性越高。


getGrayLevelNonUniformityNormalizedFeatureValue()

    4.  Gray Level Non-Uniformity Normalized (GLNN)

    GLNN衡量影像中灰度强度的变异程度，值越小说明影像强度值越相似。这是GLN标准化的版本。

getSizeZoneNonUniformityFeatureValue()

    5. Size-Zone Non-Uniformity (SZN)

    SZN衡量影像中区域体积的变异程度，值越低表明区域体积大小越一致。

getSizeZoneNonUniformityNormalizedFeatureValue()

    6. Size-Zone Non-Uniformity Normalized (SZNN)

    SZNN衡量影像中区域体积的变异程度，值越低表明区域体积大小越一致。这是SZN的标准化版本。

getZonePercentageFeatureValue()

    7. Zone Percentage (ZP)

    ZP通过计算区域数和体素数的比例来衡量ROI的粗糙程度。

    取值范围为1/𝑁𝑝≤ 𝑍𝑃 ≤ 1，数值越大说明ROI包含的的小面积区域越多（说明纹理更细致）。

getGrayLevelVarianceFeatureValue()

    8.  Gray Level Variance (GLV)

    GLV衡量区域的灰度变异程度。

getZoneVarianceFeatureValue()

    9.  Zone Variance (ZV)

    ZV 衡量区域体积大小的变异程度。

getZoneEntropyFeatureValue()

    10.  Zone Entropy (ZE)

    𝜖为任一小正数(≈ 2.2 × 10−16)。

    ZE衡量区域大小和灰度等级分布的不确定性/随机性。值越大，说明纹理模式异质性越高。

getLowGrayLevelZoneEmphasisFeatureValue()

    11.  Low Gray Level Zone Emphasis (LGLZE)
  
    LGLZE衡量低灰度值区域大小的分布情况。值越大，说明影像中低灰度值和区域越多。

getHighGrayLevelZoneEmphasisFeatureValue()
   
    12. High Gray Level Zone Emphasis (HGLZE)
   
    HGLZE衡量高灰度值区域大小的分布情况。值越大，说明影像中高灰度值和区域越多。

getSmallAreaLowGrayLevelEmphasisFeatureValue()
  
    13.  Small Area Low Gray Level Emphasis (SALGLE)
   
    SALGLE测量影像中低灰度值构成的小区域在影像中所占的比例。

getSmallAreaHighGrayLevelEmphasisFeatureValue()
   
    14. Small Area High Gray Level Emphasis (SAHGLE)
   
    SAHGLE测量影像中高灰度值构成的小区域在影像中所占的比例。

getLargeAreaLowGrayLevelEmphasisFeatureValue()
   
    15. Large Area Low Gray Level Emphasis (LALGLE)
   
    LALGLE测量影像中低灰度值构成的大区域在影像中所占的比例。

getLargeAreaHighGrayLevelEmphasisFeatureValue()
  
    16. Large Area High Gray Level Emphasis (LAHGLE)
   
    LAHGLE测量影像中高灰度值构成的大区域在影像中所占的比例。


### 2.5.6 Gray Level Run Length Matrix (GLRLM) Features

class radiomics.glrlm.RadiomicsGLRLM(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase

    Gray Level Run Length Matrix衡量灰度强度移动的长度，即用像素的数目表示具有相同灰度强度的像素连续构成的长度。在GLRLM矩阵P(𝑖, 𝑗|𝜃)中，第i行j列的元素，表示在ROI中图像强度为i，延角度𝜃走行长度为j的游程数目是多少。

    以一个二维案例举例，下述矩阵i代表一个5*5大小的影像，灰度强度分级为5：

    GLRLM角度为𝜃 = 0，意味着在平行方向测量。


    此处：
        𝑁𝑔是图像中离散强度值的数目
        𝑁𝑟是图像中离散长度的数量
        𝑁𝑝是图像中体素的数目
        𝑁𝑟(𝜃)是影像中延角度的走行的数目，等于
        P(𝑖, 𝑗|𝜃)是延任一角度的长度矩阵
        p(𝑖, 𝑗|𝜃)是标准化的长度矩阵，等于


    默认情况下，特征值是基于不同角度的GLRLM计算的，之后返回这些值的平均值。如果激活了的距离权重设置，GLRLM会基于邻域体素间的距离进行加权，然后加总并进行标准化。特征会根据以上结果进行计算。邻域体素间的距离即在相应角度中依据指定’weightingNorm’设置的距离。

    可进行下述自定义设置。

    • weightingNorm [None]: string，字符串，指定在衡量距离时使用的标准。可参考的设置如下。

        – ‘manhattan’: 一阶范数 
        – ‘euclidean’: 二阶范数
        – ‘infinity’: 无穷范数 
        – ‘no_weighting’: GLCMs采用因子1权重并求和 
        – None: 不采用权重，返回基于单独的矩阵计算的平均值
        对于提供的其它数值，会记录warning，同时会采用“no_weighting”权重。

    References
        • Galloway MM. 1975. Texture analysis using gray level run lengths. Computer Graphics and Image Processing, 4(2):172-179.
        • Chu A., Sehgal C.M., Greenleaf J. F. 1990. Use of gray value distribution of run length for texture analysis.
        Pattern Recognition Letters, 11(6):415-419
        • Xu D., Kurani A., Furst J., Raicu D. 2004. Run-Length Encoding For Volumetric Texture. International
        Conference on Visualization, Imaging and Image Processing (VIIP), p. 452-458
        • Tang X. 1998. Texture information in run-length matrices. IEEE Transactions on Image Processing
        7(11):1602-1609.
        • Tustison N., Gee J. Run-Length Matrices For Texture Analysis. Insight Journal 2008 January - June.

getShortRunEmphasisFeatureValue()

    1. Short Run Emphasis (SRE)

    SRE是一种短游程分布的度量方式，值越大，代表短的游程数目越多，纹理越细致。


getLongRunEmphasisFeatureValue()

    2. Long Run Emphasis (LRE)

    LAE是一种长游程分布的度量方式，值越大，代表长的区域数目越多，纹理越粗糙。


getGrayLevelNonUniformityFeatureValue()

    3. Gray Level Non-Uniformity (GLN)

    GLN衡量影像中灰度强度的相似程度，值越低表明图像中同质性越高。

getGrayLevelNonUniformityNormalizedFeatureValue()

    4. Gray Level Non-Uniformity Normalized (GLNN)

    GLNN衡量影像中灰度强度的相似程度，值越小说明影像强度值越相似。这是GLN标准化的版本。

getRunLengthNonUniformityFeatureValue()

    5. Run Length Non-Uniformity (RLN)

    RLN衡量影像中游程长度的相似程度，值越低表明游程长度越一致。

getRunLengthNonUniformityNormalizedFeatureValue()

    6. Run Length Non-Uniformity Normalized (RLNN)

    RLNN衡量影像中游程长度的相似程度，值越低表明游程长度越一致。这是RLNN的标准化版本。

getRunPercentageFeatureValue()

    7. Run Percentage (RP)

    RP通过计算游程数和体素数的比例来衡量ROI的粗糙程度。

    取值范围为1/𝑁𝑝≤ RP ≤ 1，数值越大说明ROI包含的的短游程越多（说明纹理更细致）。

getGrayLevelVarianceFeatureValue()

    8.	 Gray Level Variance (GLV)

    GLV 衡量灰度游走的变异程度。

getRunVarianceFeatureValue()

    9.	 Run Variance (RV)

    RV 衡量游程的变异程度。

GetRunEntropyFeatureValue()

    10.	 Run Entropy (ZE)

    𝜖为任一小正数(≈ 2.2 × 10−16)。

    RE衡量游程和灰度等级分布的不确定性/随机性。值越大，说明纹理模式异质性越高。

getLowGrayLevelRunEmphasisFeatureValue()

    11.	 Low Gray Level Run Emphasis (LGLRE)

    LGLRE衡量低灰度值的分布情况。值越大，说明影像中低灰度值越集中。

getHighGrayLevelRunEmphasisFeatureValue()

    12. High Gray Level Run Emphasis (HGLRE)

    HGLRE衡量高灰度值的分布情况。值越大，说明影像中高灰度值越集中。

getShortRunLowGrayLevelEmphasisFeatureValue()

    13. Short Run Low Gray Level Emphasis (SRLGLE)

    SRLGLE测量影像中低灰度值构成的短游程在影像中所占的比例。

getShortRunHighGrayLevelEmphasisFeatureValue()

    14. Short Run High Gray Level Emphasis (SRHGLE)

    SRHGLE测量影像中高灰度值构成的短游程在影像中所占的比例。

getLongRunLowGrayLevelEmphasisFeatureValue()

    15. Long Run Low Gray Level Emphasis (LRLGLE)

    LRLGLE测量影像中低灰度值构成的长游程在影像中所占的比例。

getLongRunHighGrayLevelEmphasisFeatureValue()

    16. Long Run High Gray Level Emphasis (LRHGLE)

    LRHGLE测量影像中高灰度值构成的长游程在影像中所占的比例。


### 2.5.7 Neighbouring Gray Tone Difference Matrix (NGTDM) Features
class radiomics.ngtdm.RadiomicsNGTDM(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase

    Neighbouring Gray Tone Difference Matrix衡量一个灰度值，与其相邻距离𝛿的邻域的灰度值平均值的差异。关于灰度i的绝对差异之和储存在矩阵中。X𝑔𝑙是体素的集合，位于(𝑗𝑥, 𝑗𝑦, 𝑗𝑧)的体素𝑥𝑔𝑙(𝑗𝑥, 𝑗𝑦, 𝑗𝑧) ∈ X𝑔𝑙，邻域的平均灰度值为：

    此处，W为位于 X𝑔𝑙中的邻域体素数量。

    以一个二维案例实例，矩阵I代表4*4的影像，具有5个离散的灰度强度，但是其中没有任何体素的强度为4，

    则NGTDM为：


    6个像素灰度值为1
    𝑠1 = |1 − 10/3| + |1 − 30/8| + |1 − 15/5| + |1 − 13/5| + |1 − 15/5| + |1 − 11/3| = 13.35
    2个像素灰度值为2
    𝑠2 = |2 − 15/5| + |2 − 9/3| = 2
    同样的对于灰度值为3和5的
    𝑠3 = |3 − 12/5| + |3 − 18/5| + |3 − 20/8| + |3 − 5/3| = 3.03
    𝑠5 = |5 − 14/5| + |5 − 18/5| + |5 − 20/8| + |5 − 11/5| = 10.075

    此处：
    𝑛𝑖 是Xgl中灰度强度值为I的体素的数量。
    𝑁𝑣,𝑝是Xgl中总的体素的数量，等于∑︀ 𝑛𝑖（i.e. 标记区域内体素的数量；至少有一个近邻单位。）𝑁𝑣,𝑝≤NP，Np是ROI中总的体素的数量。
    P𝑖 是灰度强度的概率，等于𝑛𝑖/𝑁𝑣
    S𝑖 是关于灰度i的绝对差异之和
    𝑁𝑔 是离散灰度值的数目
    𝑁𝑔,𝑝 是灰度强度概率不等于0的灰度强度的数目


    可以进行如下设置

        • distances [[1]]: List of integers，整数值构成的列表。用于衡量沿某一角度，中心voxel及其相邻voxel间的距离。

    参考
        • Amadasun M, King R; Textural features corresponding to textural properties; Systems, Man and Cybernetics, IEEE Transactions on 19:1264-1274 (1989). doi: 10.1109/21.44046


getCoarsenessFeatureValue()

    计算和返回粗糙程度。

    Corseness是中心体素与其邻域之间平均差异的测度，是空间变化率的指标。值越高，说明变化率越小，局部纹理越一致。

    N.B 可能等于0（在完全一致的影像中）。在这种情况下，会返回任意值10^6。


getContrastFeatureValue()

    计算并返回Contrast。

    Contrast是空间强度变化的指标，但同样依赖于整体的灰度动态变化范围。当动态变化范围和空间变化率都高时，Contrast亦高，i.e. 体素间及其邻域间的差异很大，灰度范围很大的影像

    N.B. 在完全同质化的影像中，𝑁𝑔,𝑝 = 1，会导致结果除以0。在这种情况下，会返回0。


getBusynessFeatureValue()
    
    计算并返回Busyness。

    衡量某一像素至其邻域变化的度量方法。值越高，说明像素至其邻域的强度变化越频繁。

    N.B. 如果𝑁𝑔,𝑝=1，则𝑏𝑢𝑠𝑦𝑛𝑒𝑠𝑠 = 0/0。在这种情况下，返回0，表明这是一个完全同质化的区域。


getComplexityFeatureValue()

    计算并返回Complexity。

    当一个影像中具有很多基本成分时，认为这个影像很复杂，i.e.影像为非均质化的，具有很多强度变化。


getStrengthFeatureValue()

    计算并返回Strength。

    Strength是影像中基本成分的度量方式。值越高，说明基本成分越容易发现和易于看见，i.e. 灰度强度变化缓慢但灰度强度粗糙程度较大的图像。

    N.B. 可能等于0（在完全同质化的影像中）。这种情况下，返回0。


### 2.5.8 Gray Level Dependence Matrix (GLDM) Features
class radiomics.gldm.RadiomicsGLDM(inputImage, inputMask, **kwargs)

Bases: radiomics.base.RadiomicsFeaturesBase

    Gray Level Dependence Matrix是影像中灰度依赖程度的测度。灰度依赖定义为在𝛿距离上与中心体素依赖的邻域体素的数量。如果|𝑖 − 𝑗| ≤ 𝛼，则认为具有灰度强度𝑗的相邻体素与某一中心体素𝑖依赖。在灰度相关矩阵P(𝑖, 𝑗)中，第𝑖行𝑗列的元素，代表影像中具有𝑗个依赖体素的灰度等级为𝑗的体素的数量。

    以一个二维案例举例，下述矩阵i代表一个5*5大小的影像，灰度强度分级为5。

    对于𝛼 = 0，𝛿 = 1，GLDM为（译者著：灰度等级i的中心像素，本身也作为依赖像素计算。）

    此处：
    N𝑔是影像中离散化强度值的数目
    N𝑑是影像中离散化依赖大小的数目
    N𝑧是影像中依赖区域的数目，等于
    P(𝑖, 𝑗)是依赖矩阵
    P(𝑖, 𝑗)是标准化的相关矩阵，定义为

    Note：因为允许有不完整的区域，因此在ROI中每个体素均有一个依赖区域。因此，N𝑧=N𝑝，N𝑝是影像中体素的数量。由于N𝑧=N𝑝，Dependec Pecentage 和GLLNN被移除。首先是因为他们计算结果总为1，其次因为在数学上他们等于first order - Uniformity (参阅getUniformityFeatureValue())。数学证明，参考这里。


    可进行下属设置

    • distances [[1]]: List of integers，整数值构成的列表。用于衡量沿某一角度，中心voxel及其相邻voxel间的距离。

    • gldm_a [0]: float，浮点数值，判断相关的界值。与灰度水平i依赖的邻域体素灰度值j须满足|𝑖 − 𝑗| ≤ 𝛼。


    参考
    • Sun C, Wee WG. Neighboring Gray Level Dependence Matrix for Texture Classification. Comput Vision, Graph Image Process. 1983;23:341-352


getSmallDependenceEmphasisFeatureValue()

    1. Small Dependence Emphasis (SDE)

    SDE是一种小依赖分布的度量方式，值越大，代表依赖越小，纹理越不均匀。


getLargeDependenceEmphasisFeatureValue()

    2. Large Dependence Emphasis (LDE)
    
    LDE是一种大依赖分布的度量方式，值越大，代表依赖越大，纹理越均匀。


getGrayLevelNonUniformityFeatureValue()

    3. Gray Level Non-Uniformity (GLN)

    GLN衡量影像中灰度强度的相似程度，值越低表明图像中同质性越高。


getGrayLevelNonUniformityNormalizedFeatureValue()

    DEPRECATED.	 Gray Level Non-Uniformity Normalized (GLNN)
    Warning：该特征已经被废弃了，因为数学上等于First Order – Uniformity getUniformityFeatureValue()。激活此特征会记录一个Deprecation-Warning（不会打断其它特征的提取），不会为此特征计算任何值。

getDependenceNonUniformityFeatureValue()

    4. Dependence Non-Uniformity (DN)

    DN衡量影像中依赖的相似程度，值越低表明依赖越一致。

getDependenceNonUniformityNormalizedFeatureValue()

    5. Dependence Non-Uniformity Normalized (DNN)

    DNN衡量影像中依赖的相似程度，值越低表明依赖越一致。这是DN的标准化版本。

getGrayLevelVarianceFeatureValue()

    6. Gray Level Variance (GLV)

    GLV 衡量灰度强度的变异程度。

getDependenceVarianceFeatureValue()

    7. Dependence Variance (DV)

    DV 衡量依赖大小的变异程度。

getDependenceEntropyFeatureValue()

    8. Dependence Entropy (DE)

    getDependencePercentageFeatureValue()

    DEPRECATED. Dependence Percentage

    Warning：该特征已经被废弃了，因为其结果永远为1。激活此特征会记录一个Deprecation-Warning（不会打断其它特征的提取），不会为此特征计算任何值。

getLowGrayLevelEmphasisFeatureValue()

    9. Low Gray Level Emphasis (LGLE)

    LGZE衡量低灰度值的分布情况。值越大，说明影像中低灰度值越集中。

getHighGrayLevelEmphasisFeatureValue()

    10. High Gray Level Emphasis (HGLE)

    HGLE衡量高灰度值的分布情况。值越大，说明影像中高灰度值越集中。

getSmallDependenceLowGrayLevelEmphasisFeatureValue()

    11. Small Dependence Low Gray Level Emphasis (SDLGLE)

    SDLGLE测量影像中低灰度值构成的小依赖在影像中所占的比例。

getSmallDependenceHighGrayLevelEmphasisFeatureValue()

    12. Small Dependence High Gray Level Emphasis (SDHGLE)

    SDHGLE测量影像中高灰度值构成的小依赖在影像中所占的比例。

getLargeDependenceLowGrayLevelEmphasisFeatureValue()

    13. Large Dependence Low Gray Level Emphasis (LDLGLE)

    LDLGLE测量影像中低灰度值构成的大依赖在影像中所占的比例。

getLargeDependenceHighGrayLevelEmphasisFeatureValue()

    14. Large Dependence High Gray Level Emphasis (LDHGLE)

    LDHGLE测量影像中高灰度值构成的大依赖在影像中所占的比例。


## 2.6 Excluded Radiomic Features  排除的影像组学特征

PyRadiomics不支持一些众所周知的特征。这些特征列举在这里以建立一个完整的回顾，并说明PyRadiomics不包含这些特征的原因。


### 2.6.1 Excluded GLCM Features  排除的GLCM特征


已经包含的特征和类的定义，参考Gray Level Co-occurrence Matrix (GLCM) Features。


**Sum Variance**

Sum Variance是一种衡量异质性的方法，它将更高的权重放在与均值偏离更多的邻域强度对上。

这个特征被移除，因为其在数学上与Cluster Tendency（参见getClusterTendencyFeatureValue())一致。

数学证明过程如下：


**Dissimilarity**

Dissimilarity是局部强度变异程度的度量方式，定义为邻域对之间的平均绝对差。数值越大说明邻域体素间的强度差异越大。

这个特征被移除，因为其在数学上与Difference Average (参考getDifferenceAverageFeatureValue())一致。

数学证明过程如下：


### 2.6.2 Excluded GLDM Features   排除的GLDM特征
 
已经包含的特征和类的定义，参考Gray Level Dependence Matrix (GLDM) Features。

**Dependence percentage**

Dependence percentage是具有依赖域体素数目与影像中总体素数目的比值。因为PyRadiomics允许不完全的相关域，所有的体素均有相关域，即Nz=Np，会导致该结果永远计算为1。


**Gray Level Non-Uniformity Normalized**

衡量影像中灰度强度相似性的方法，低GLNN值说明强度值相似。这是一个GLN标准化的版本。

这个公式被移除，因为根据GLDM矩阵的定义（允许不完全域），这个特征等于first order类中的Uniformity特征（参考getUniformityFeatureValue()）

数学证明过程如下：


## 2.7 Contributing to pyradiomics  帮助pyradiomics

有多种方式可以改进pyradiomics。如果有什么不清楚可以首先参考文件，然后让我们知道以便做的更好。

+ 通过[pyradiomics email list](https://groups.google.com/forum/#!forum/pyradiomics)询问。
+ 递交你用来提取特征的parameter file参数配置文件。
+ 递交一个特征请求或错误，或者参与[pyradiomics issue tracker](https://github.com/AIM-Harvard/pyradiomics/issues)讨论。
+ 递交一个[Pull Request](https://github.com/AIM-Harvard/pyradiomics/pulls)提高pyradimoics及他的文档。

我们鼓励任何形式的Pull Request，从测试和文档的补丁到可以讨论的未成熟的想法。


### 2.7.1 The PR Process, Circle CI, and Related Gotchas  PR Process，Circle CI，Related Gothas

**How to submit a PR ?  如何传递PR？**

如何你是pyradiomics开发的新手，并且你没有pyradimics repository的权限，请参考：


1. Fork and clone储存库。
2. 创建一个分支。
3. 推送分支至你的GITHUB fork。
4. 创建一个Pull Request


此处与GitHub flow指南中提到的Fork & Pull Model部分一致。

如果你有pyradiomics repository权限，你可以轻松推送你的分支至主存储库，并且创建Pull Request。这与Shared Repository Model（的方法）一致，会加速其它开发者检查你的主题而无需configure a remote。这也会简化你co-developing一个分支时的流程。

当传递一个PR时，确定添加一个cc: @Radiomics/developers评论引起pyradiomics 开发者们的注意。根据评审者的评论，你可能需要修改你的补丁。


**How to integrate a PR ?  如何整合PR？**

整合你的贡献是相对简单的，这里是检查清单：

+ 必要时，你所进行的更改须包含一个更新文档

        - 有关modules，calsses，fuctions的文档分别保存
        - 一般性的文档保存在docs文件夹中
        - 在自动生成的文档中添加新的模块。参考此处获取更多在文档中添加新模块的信息。

+ 在Next Release中的changlog部分添加你所做的改变。
+ 通过所有测试。
+ 达成共识。这一般意味着需要至少一评位审者审阅并支持你所做的变化或添加了一个LGTM评论，即Looks Good to Me首字母的缩写。


接下来，有两种情形：

+ 你没有推送权限：pyradiomics核心开发者会整合你的PR。
+ 你具有推送权限：点击 “Merge pull request”按钮。


然后，点击之后出现的“Delete branch”按钮。


**Automatic testing of pull requests  自动测试Pull requests**

每次推送提交时，都会使用CircleCI, TravisCI and AppVeyor测试所有的Pull request。Github UI会限制使用者合并PULL REQUEST，直到建造者返回所有测试成功通过和没有问题的结果。测试包括以下类别：

+ flake8，检测代码的一致性。参考flake8和.editorconfig 的格式，PEP8格式例外。

+ 如果某一特征类含有_calculateCMatrix()函数，并将其作为一个C增强类，则C拓展输出的结果会与python计算的输出结果相比较。机器的精度误差允许范围在1e-3之间。

+ 所有特征和特征类别在类水平和特征定义水平有文档字符串。

+ 从五个测试案例中提取的特征都有一个基线水平，计算出的特征与这些基线相差3%范围内（机器误差范围内）。


### 2.7.2 Submitting a parameter file  传递参数配置文件

PyRadiomics不同的输入需要不同的设置。我们鼓励使用者分享他们的参数配置文件，以帮助其他人使用最好的设置为其案例提取特征。

**How to submit your parameter file?  如何传递参数配置文件？**

参数配置文件储存在存储库examples/exampleSettings文件夹下。如果你希望传递你的参数配置文件，你可以通过pull request 添加你的文件。为了帮助你通过，以下是个小小的检查清单：

+ 文件名称至少应该含有用于什么模式（e.g. MR）使用，以及可选的部位（e.g. prostate）

+ 确保文件有正确的拓展名。

+ 在参数配置文件中使用注释，简要说明你使用的情况。

当你打开PR传递文件后，会自动检测其合理性。你不用特别指定你文件的位置，参数配置文件会自动在exampleSettings文件中检测到。如果需要，你也可以手动使用bin/testParams.py检查你的参数配置文件。

## 2.8 Developers  开发者

这一部分包含如何添加和自定义PyRadiomics中包含的特征类和滤波的信息。PyRadiomics会在工具箱初始化时遍历所有的特征类别和输入的影像类型。可以分别通过使用getFeatureClasses() 和getImageTypes()函数在全局radiomics命名空间内获取。在每一特征类初始化时会遍历其中的每一个特征。也可参阅contributing guidelines。


### 2.8.1 Signature of a feature class  特征类的签署

每一个影像特征类分别定义在单独的模块中，模块名称通常以特征类名称命名。（e.g.如果tex.py与某一特征类的标签匹配，则在PyRadiomics工具箱中可以获取tex影像特征类。）在模块中，类的定义应符合以下签署（方式）：

~~~
[required imports]
from radiomics import base
class Radiomics[Name](base.RadiomicsFeaturesBase):

"""
Feature class docstring
"""

def __init__(self, inputImage, inputMask, **kwargs):
    super(Radiomics[Name], self).__init__(inputImage, inputMask, **kwargs)
    # Feature class specific init

def get[Feature]FeatureValue(self):

    """
    Feature docstring
    """

    # value = feature calculation using member variables of RadiomicsFeatureBase and this class.
    return [value]
~~~

+ 首先应导入特征类需要使用的软件包。不使用的导入语句应该移除（如果遇到了不使用的导入语句，或导入的语句未参照appnexus格式组织结构，flake3会失败）

+ 类名称应以类的名称之后衔接“Radiomics”命名（通常与模块的名称一致。然而，这个名称不应用于其它任何地方，但可以任意命名）

+ 特征类应该从base.RadiomicsFeaturesBase类中继承（直接或间接），这是一个定义所有特征类共同交互方式的总类。

+ 额外的初始化步骤应该通过_int_函数调用。默认启动的变量，参考Feature Class Base.

+ 需要文档！在特征类级别（特征类文档字符串）以及在每一特征级别（特征文档字符串）均需要。

+ 如果特征类需要C拓展增强矩阵计算功能，则应该通过test_matrices测试，矩阵计算应该采用以下方式实现：

    - 使用C拓展计算矩阵的功能应该定义在一个称作_calculateMatrix的函数中。

    - 计算矩阵的函数除了self参数外，不接受任何其它参数，并将完全处理后的矩阵以Numpy array的形式返回。

    - 完全处理后的矩阵在特征类中应指定给一个命名为P_\[Name]的变量，其中\[NAME]应与特征类的名称（即模块的名称）相同。（e.g. 在GLCM特征类中，矩阵存储在p_glcm变量中。）

+ 通过base class创建了一个专用的子类、特征类logger（i.e. the ‘radiomics.tex’ logger即tex特征类的logger）。在特征类中作为self.logger。由特征类生成的任何记录消息都应使用该Logger，以确保类的层次结构正确的反应在生成的记录中。（i.e. self.logger.debug（‘message’）生成debug记录。）


### 2.8.2 Adding the baseline  添加基线

在测试阶段，计算后的特征会与固定的基线做比较。如果你引入了一个新类，则必须添加基线，否则测试会失败。幸运的是，为一个新类添加基线相当简单：只需要运行tests文件夹下的add_baseline.py脚本即可。如果你改变了某一特征，并需要重新为该类建立基线，则使用类名称作为参数运行该脚本。（e.g. python add_baseline.py glcm）


### 2.8.3 Signature of individual features  特征签署

使用特征类中get\[Name]FeatureValue(self)函数为每一个单独的特征签署，其中\[name]即特征的名称（在特征类水平上是独一无二的）。不传递任何参数，结果会返回一个常量。self参数代表实例化的特征类函数，并将特征函数识别为非静态函数。


### 2.8.4 Signature of an image type  影像类型签署

所有imge types定义在imageoperations module模块中，并通过标签get\[Name]Image(inputImage, inputMask, \**kwargs)标识。此处\[name]代表独一无二的image type影像类型名称，同样用来在特征提取过程中识别影像的类型。影像类别函数的输入由imputImage和imputMask组成，即分别代表原始image和mask的SimpleiTK Image对象，以及自定义的从派生影像中提取特征的设置的**kwargs参数组成。

一个或多个的派生影像使用yield语句生成：yield derivedImage, imageTypeName, kwargs。此处，derivedImage是SimpleITK影像对象，代表滤波处理过的image，imageTypeName是结果中使用该滤波生成的特征的独一无二的字符串标识，kwargs是为提取过程添加的自定义设置。（**kwargs作为输入传递，没有双星号）。多种影像可经多重yield语句，或循环形式的yield语句返回。请注意，每次调用yield时仅会生成一种派生影像，且ImageTpyeName对于每种派生影像都是独一无二的。派生的影像必须有相同的维度，并占据相同的物理空间以和mask兼容。

### 2.8.5 Progress Reporting

当在full-python模式操作时，纹理矩阵的计算需要花费些时间。因此PyRadiomics提供报告计算GLCM和GLSZM进程的可能。这仅在full-python模式下，且setVerbosity()设置为INFO或DEBUG时生效。默认情况下，不提供任何信息，并且也不会报告矩阵计算的进程。

为了激活进程报告，radiomics.progressReporter变量应该设置成一个类对象（而不是一个实例），应该符合以下签署：

1. 接收迭代并将其作为首个位置参数，以及一个关键词参数（'desc'）用以指定展示的标签

2. 可以通过‘with’语句使用 (i.e. 具有 __enter__ 和__exit__ 功能)

3. 可迭代(i.e. a至少指定一个__iter__函数，该函数在初始化时传递的可迭代对象上迭代).


也可创建你自己的进程报告。为了达到该效果，额外指定一个函数_next_，具备_iter_功能返回self。\__next__函数不接受参数，并返回对可迭代对象\__next__函数的调用。（i.e. 返回 self.iterable.\__next\__()）。任何结果/进程报告都可以在返回语句前插入此函数中。


在radiomics\__init__.py定义了一个哑进程报告，当在full-python模式下计算时会使用，但是进程报告没有被激活（verbosity > INFO）或progressReporter变量没有设置的时候不会。

设计一个自定义的进程报告，可以采用下述代码并作为progressReporter使用。

~~~
class MyProgressReporter(object):
    def __init__(self, iterable, desc=''):
        self.desc = desc # A description is which describes the progress that is reported
        self.iterable = iterable # Iterable is required

# This function identifies the class as iterable and should return an object which exposes
# the __next__ function that should be used to iterate over the object

    def __iter__(self):
        return self # return self to 'intercept' the calls to __next__ to insert reporting code.

    def __next__(self):
        nextElement = self.iterable.__next__()
        # Insert custom progress reporting code here. This is called for every iteration in the loop
        # (once for each unique gray level in the ROI for GLCM and GLSZM)
        # By inserting after the call `self.iterable.__next__()` the function will exit before the
        # custom code is run when the stopIteration error is raised.
        return nextElement

    # This function is called when the 'with' statement is entered

    def __enter__(self):
        print (self.desc) # Print out the description upon start of the loop
        return self # The __enter__ function should return itself

    # This function is called when the 'with' statement is exited

    def __exit__(self, exc_type, exc_value, tb):
        pass # If nothing needs to be closed or handled, so just specify 'pass'
~~~

### 2.8.6 Using feature classes directly  直接使用特征类

+ 这是一个直接使用特征类的案例，绕过了影像组学特征提取类的检查和预处理，并不作为一种标准的使用方法。

+ （LINUX）为了使用源代码，将pyradiomics添加至环境变量PYTHONPATH中（如果已安装PyRadiomics则不需要）

    - setenv PYTHONPATH /path/to/pyradiomics/radiomics

+ 启用python交互式进程。

    - python


+ 导入必要的类

~~~
from radiomics import firstorder, glcm, imageoperations, shape, glrlm, glszm, getTestCase
import SimpleITK as sitk
import six
import sys, os
~~~

+ 设置数据文件夹变量
~~~
dataDir = '/path/to/pyradiomics/data'
~~~

+ 你会在文件夹中找到brain1_image.nrrd and brain1_label.nrrd文件。

+ 使用SimpleITK读取brain image和mask

~~~
imageName, maskName = getTestCase('brain1', dataDir)
image = sitk.ReadImage(imageName)
mask = sitk.ReadImage(maskName)
~~~

+ 计算first order features

~~~
firstOrderFeatures = firstorder.RadiomicsFirstOrder(image,mask)
firstOrderFeatures.enableAllFeatures() # On the feature class level, all features are disabled by default.
firstOrderFeatures.calculateFeatures()
for (key,val) in six.iteritems(firstOrderFeatures.featureValues):
print("\t%s: %s" % (key, val))
~~~
+ 参考Radiomic Features了解更多你可以计算的特征。

### 2.8.7 Addtional points for attention  需要注意的其他细节

**Code style  代码样式**

为了保证PyRadiomics代码的一致性以及可读性，强制使用某些规则。这些都是使用flake8进行连续测试的一部分，也可参考存储库根目录中的.flake8配置文件。为了保持一致性的代码样式，在根目录提供了一个.editorconfig文件。

模块名称应保持小写，不使用下划线或空格。类名称，函数名称，以及变量应该使用骆驼拼写法声明，类名称的首字母采用大写其余采用小写。Private helper函数（不应该包含在文档中）应该以“_”前缀声明，这是为了与Python风格一致以标记他们为“Private”，会在生成的文档中自动排除他们。

**Documentation**

PyRadiomics文档是基于docs文件夹中的静态文件和Python代码文件中的字符串文档自动生成的。当添加一个新的特征类时，也会在静态文件（features.rst）中添加该特征类的描述。依据该方式处理后，sphinx会处理剩下的内容。一个特征类会以以下方式添加：

~~~
<Class Name> Features
---------------------
.. automodule:: radiomics.<module name>
    :members:
    :undoc-members:
    :show-inheritance:
    :member-order: bysource
~~~

特征类的信息(e.g. 特征矩阵是如何计算的)应作为一个整体在特征的文档字符串中提供。每个特征的定义，包括数学公式，应该在特征函数的文档中提供。不需要某个模块的文档。

在测试期间需要并检查在类水平和每一特征水平的字符串文档。如果没有字符串文档则会就导致测试失败。

如果你编辑文档，或你希望测试你添加的类的文档是如何生成的，可以在本地生成sphinx文档：
1. pip install sphinx
2. pip install sphinx_rtd_theme
3. 在docs文件夹中运行这条命令 make html
4. HTML版本的Sphinx文档根会出现在_build/html/index.html中。



**Testing  测试**

为了确保PyRadiomics提取特征的一致性，在每次提交后都会使用连续测试检测Py Radiomics源代码。这些测试定义在test文件夹中，被用在以下环境中运行测试：

    • Python 2.7 64 bits (Windows, Linux and Mac)

    • Python 3.4 64 bits (Windows and Linux)

    • Python 3.5 64 bits (Windows and Linux)

注意：因为Python3中SimpleTIK软件包的一些问题，对于MAC中Python 3的测试现在关闭了.

这里有三个PyRadiomics测试脚本。第一个测试是test_cmatrices，用来测试C拓展计算的矩阵是否与Python计算的结果匹配。机器精度误差在1e-3之间。第二个测试是test_docstrings,用来在上述描述中是否有缺失的文档。最后一个并且也是最重要的测试是test-features，用来比较PyRadiomics计算生成的特征与5个案例已知的基线特征的一致性。这些测试案例和基线储存在存储库中data文件夹中。这确保了代码的改变没有悄悄的改变了这些特征的计算。

为基线添加一个新的特征类，需要运行储存在bin文件夹中的addClassToBaseline.py脚本。这个脚本会检测pyradiomics中的特征类是否没有基线值。如果找到了这样的特征，并可以在full-python模式下计算这些特征，则在基线文件中添加新的基线值。这些基线文件需要包含在储存库中并重新提交。


## 2.9 pyradiomics labs

Pyradiomics labs是储存库中的一部分，用以收集一些exploratory/experimental特性，但是不作为核心功能的一部分。我们欢迎使用者反馈使用这些功能。这部分代码和特性以后可能会发生变化。

### 2.9.1 pyradiomics-dcm

**About**

这是一个支持从DICOM数据中使用pyradiomics的实验性脚本。

该脚本会将包含单个DICOM影像的文件夹作为输入，文件名指向一个DICOM Segmentation Image（DICOM SEG）对象。

脚本会使用plastimatch 或 dcm2niix，将DICOM影像转换成一个合适的呈现形式。


**Why？  为什么？**

+ 医学影像经常是DICOM格式，而pyradiomics使用者在使用DICOM数据时经常会寻求帮助。

+ 在TCIA上有公共收集的数据，以DICOM SEG存储分割数据。

+ 使用DICOM表示影像组学特征

    - 为与特征一起存储的属性，引入标准化的形式。

    - 允许将计算结果，与描述分析的区域解剖结构的本体，以及特征本身联系起来（e.g. 由脚本生成的SR文档将使用IBSI命名法，来描述在pyradiomics中实现的与IBSI对应的功能）。

    - 允许参照（通过独一无二的标识符）DICOM影像系列和DICOM分割进行特征计算

    - 使images，segmentations，features的呈现方式具有一致性（i.e. 可以为所有的数据类型使用同一个数据管理系统）

    - 不避免在 不能使用DICOM-aware - dcmqi 转换 DICOM segmentations 和 DICOM SR 以及测量结果至 non-DICOM表示的软件中 使用结果(ITK-readable image格式的分割, JSON格式的测量值); 可以使用一个单独的工具以制表符分隔的形式存储在SRs中的DICOM属性和测量值:https://github.com/QIICR/dcm2tables


**Prerequisites  前提条件**

+ plastimatch或dcm2niix，用于影像体积重构

+ dcmqi (build from fedb41 or later),用于读取DICOM SEG并转换成适合pyradiomics的形式，以及将结果转换成DICOM结构的报告，比如SR TID 1500

+ 在使用该脚本之前，你应该将你的DICOM数据分类依照单独的系列存储于不同的文件夹中。你会发现这个工具有用：https://github.com/pieper/dicomsort

+ 如果你的分割并不是以DICOM SEG形式存储，你可以使用dcmqi生成这些分割的标准表现形式：https://github.com/QIICR/dcmqi。


**Usage 使用**

通过命令行使用的示例
~~~
$ python pyradiomics-dcm.py -h
usage: pyradiomics-dcm.py --input-image <dir> --input-seg <name> --output-sr <name>

Warning: This is a "pyradiomics labs" script, which means it is an experimental feature in development!
The intent of this helper script is to enable pyradiomics feature extraction directly from/to DICOM data.
The segmentation defining the region of interest must be defined as a DICOM Segmentation image.
Support for DICOM Radiotherapy Structure Sets for defining region of interest may be added in the future.

    optional arguments:
        -h, --help show this help message and exit
        --input-image-dir Input DICOM image directory
                        Directory with the input DICOM series. It is expected
                        that a single series is corresponding to a single
                        scalar volume.
        --input-seg-file Input DICOM SEG file
                        Input segmentation defined as aDICOM Segmentation
                        object.
        --output-dir Directory to store the output file
                    Directory for saving the resulting DICOM file.
        --parameters pyradiomics extraction parameters
        --temp-dir Temporary directory

        --features-dict Dictionary mapping pyradiomics feature names to the IBSI defined features.
        --volume-reconstructor Choose the tool to be used for reconstructing image volume from the DICOM image series. Allowed options are plastimatch or dcm2niix (should be installed on the system). plastimatch will be used by default.
~~~

**Sample invocation**

**Questions？问题**

通过pyradiomics email list传递你的反馈和问题。

**References**

## 2.10 Frequently Asked Questions  常见问题解答

### 2.10.1 Feature Extraction: Input, Customization and Reproducibility  特征提取：输入，自定义设置和可重复性

Does PyRadiomics adhere to IBSI definitions of features? PyRadiomics对特征的定义与IBSI相同么？

对于大多数的部分，是的。

PyRadiomics的发展同样和IBSI团队标准化的努力有关。但是，在特征提取方面pyradiomics和IBSI文档的定义之间还是有些差异。这主要出现在一些存在同等的合理性选择的时候。在这些情况下，PyRadiomics倾向于一种选择，而IBSI标准则推荐另外一种。基于PyRadiomics发展一致性的原因，我们倾向于不改变PyRadiomics实现过程，而在文档中记录这些差异。

最值得注意的是在灰度离散化（仅固定bin大小类型）和重采样方面的差异。这些差异不能仅通过自定义设置校正，需要通过定制函数替换：

+ Binning：当使用固定bin width (AKA IBSI: FBS, Fixed Bins Size)执行灰度离散化并且使用Resegmentation设置时，如果是absolute-resegmentation，IBSI是从resegmentation的最小值计算bin分组的边缘，当采用sigma-resegmetation时，使用最小强度值。

    在PyRadiomics中，使用固定bin width进行灰度离散化时，bin边缘值从0起始，确保最低的灰度值包含在第一个bin分组中。而与resegmentation无关。


+ Resampling  重采样

    - Alignment of the grid 网格配准：在IBSI，重采样配准依据影像中心的配准。在Pyradiomics中，我们通过体素的原点进行配准。这会在插值器结果上引起轻微的差异，以及在重采样的影像和ROI大小上轻微的差异，并会进一步引起提取的特征具有轻微的差异。

    - Gray value rounding 灰度值取整：在IBSI中，如果原始影像强度来自于一个低精细度的类型，则重采样后的值（浮点数值，一般为64-bit）也应重采样至一个相似的空间分辨率。在IBSI phantoms情况下，会重采样至最接近的整数值。PyRadiomics不会这么做，因为差异可能很小，反而会增加复杂性，而不会有益于提取特征。尤其是考虑到灰度值在计算大多数（不包括firtorder）特征之前都是离散的。如果采用了某种标准化，灰度值的平均值也会发生变化。此处会引发差异，因为小数取整的过程中会导致一个体素被分配至不同的bin分组，这会导致未来巨大的差异。尤其在小ROI中。

    - Mask resampling Mask 重采样：在IBSI中，可以选择不同的插值器对掩膜进行重采样，并对二进制掩膜进行额外的阈值提取。这仅在mask限制为0和非0的情况下生效。PyRadiomics同样支持带有不同值标签的mask，允许从同一个mask中的以不同的值标记的ROI中提取特征。为了阻止任何不正确的重分配，PyRadiomics强制将mask重采样至最近邻。

接下来，同样有一些差异可以通过自定义设置解决，这仅适用于Configuration E，此时absolute 和sigma resegmentation均执行。在PyRadiomics中，两种类型均可实施，但是在某一次中仅能执行一种。为了模拟实施两种类型，我计算了重分割后的绝对范围，并将其作为绝对重分割范围：[-718,400]。

最后，在PyRadiomics和IBSI计算firtorder特征kurtosis时，存在差异。IBISI计算Excess Kurtosis，等于Kurtosis-3。Pyradiomics计算的Kurtosis，与IBSI相比总是+3。差异3来源与于高斯分布的Kurtosis值为3。


总结，PYradiomics结果与IBSI基准的差异的原因：

+ Configuration C：由于灰度强度值离散化和重采样的差异。
+ Configuration D：由于重采样的差异。
+ Configuration E：由于重采样和重分割的差异。


**What about gray value discretization? Fixed bin width? Fixed bin count?  灰度离散化如何？固定bin width？ 还是固定bin count?**

当前，尽管很多研究倾向于采用一个固定的bin count而不是一个固定的bin width，但是没有坚实的证据表明其中哪一个无论在何时都会更好。因此在PyRadiomics中固定bin cout(binCount)和 bin width(binWidth，默认)这两种方式我们都可以实现。

将固定bin width作为默认参数，是因为在PET有关的实验中证实，采用固定bin width有助于特征采集的重复性。此外，还可以通过以下案例说明：比如输入两个影像及2个ROIs，其中第一个的影像灰度值范围为0-100，第二个为0-10。如果使用固定bin count，则1个离散灰度分布的意义就不同了（在第一案例中可能代表10，在第二个案例中代表1）。这意味着你正在观察不同对比程度的纹理。

这个案例的假设是基于原始灰度值在两幅影像中代表的含义是一致的，这在具有明确的/绝对的灰度数值的影像中，是正确的。但是，在一些任意的/相对的灰度影像中，则不一定正确。在后一种情况中，我们仍推荐一个固定的bin width，但是需要进行额外的预处理（e.g. 标准化）以保证灰度值的可匹配性。这里也可以使用固定的bin count，但是计算后的特征仍然很容易受到影像中灰度值范围的影响，或受到灰度值缺乏可比性的干扰。此外，不考虑灰度离散化，也需要采取措施以保证更好的对比度，因为firt order features主要基于原始灰度值计算（不需要离散化）。

最后，还有关于如何设置bin width的问题。再一次，目前没有明确的指南说明最好的bin width是什么。我们尝试通过这种方式选择一个bin width，使结果中的bins数量在30-130之间，在文献中这个范围相对于固定的bin count，表现出了良好的可重复性和效果。在不同强度范围的ROI中均可采用，并保留了纹理特征的信息（以及病变间的可比较性）。


**What modalities does PyRadiomics support? 2D? 3D? Color?  PyRadiomics支持哪种模式？2D?3D?彩色？**

PyRadiomics不是针对某一模态开发的。PyRadiomics可以处理多模态的数据，尽管针对不同模态的数据可能会有不同的优化设置。这里有一些关于输入内容的限制条件：

1. Gray scale volume：PyRadiomics暂时不支持从彩色影像，或具有复杂数值的影像中提取特征。在这些案例中，每一个像素/体素拥有多个数值，PyRadiomics不知道你想如何组合他们。可以通过选择某一通道将其作为输入：

~~~
import SimpleITK as sitk

from radiomics import featureextractor

# Instantiate extractor with parameter file
extractor = featureextractor.RadiomicsFeatureExtractor(r'path/to/params.yml')

# Set path to mask
ma_path = 'path/to/maskfile.nrrd'
label = 1 # Change this if the ROI in your mask is identified by a different value

# Load the image and extract a color channel
color_channel = 0
im = sitk.ReadImage（r'path/to/image.jpg'）
selector = sitk.VectorIndexSelectionCastImageFilter()
selector.SetIndex(color_channel)
im = selector.Execute(im)

# Run the extractor
results = extractor.execute(im, ma_path, label=label)
~~~

2. File format：当前，Pyradiomics需要以采用指向image/mask文件的字符串的形式或以simpleITK image 对象输入（仅在交互模式中可能）的方式载入image和mask。当，如使用DICOM文件时，在提取特征前，这些拆分的文件需要首先组合成一个volume，比如转换成NRRD或NIFTII的模式，或通过一个Python脚本读取DICOM并过该脚本调用PyRadiomics。也可参阅
What file types are supported by PyRadiomics for input image and mask?。

3. Dimensionality：Pyradiomics支持2D 和3D影像输入，但是需注意shape特征类仅支持3D形态描述，而shape2D仅支持2D形态描述。如果是一个3D volume，但是采用的是单片分割，并且想要在结果中包含2D形态描述，则强制使用shape2D并设置force2D=True。这允许你从3D volume使用单片分割提取2D形态特征（但在分割是采用多片分割表达volume分割时会失败）。

**What file types are supported by PyRadiomics for input image and mask?  PyRadiomics支持哪种类型的image和mask输入？**

PyRadiomics使用SimpleITK进行文件导入和处理。因此，所有SimpleITK支持的影像均可作为PyRadiomics的输入。请注意，仅需要为image/mask提供一个文件地址。

如果你的影像是DICOM格式，事情会变得更复杂。如果你想处理一个储存在DICOM格式中的2D影像切片，你可以将其作为任何其它格式处理。然而，如果你处理的是一个具有体积的数据，你首先要确认你的DICOM文件是关于某一单个影像的系列文件。如果你不确定，你可以将数据按照一个系列一个文件夹进行分类，比如用，dicomsort。之后你可以使用plstimatch convert 或dcm2niix将DICOM系列转换成ITK可读的体积格式。

如果你的label也储存在DICOM格式中，这会有些不同。首先，检查具有label的数据的模式。你可以通过使用dcmdump，在命令行中输入“Modality”的方式进行检查。可以在这里找到这个工具的二进制工具包（如果你想在Atom editor中更方便的查看DICOM，你同样也可以使用dicom-dump软件包）

+ 如果模态是image，则使用plastimatch 或dcm2niix将image转换为3D volume

+ 如果模态是RT，则使用platimatch将结构轮廓转换为3D volumes。

+ 如果模态是SEG，则使用dcmqi将体素分割转换为3D volumes。

我们提供了一个实验性的脚本pyradiomics-dcm，可以自动化处理这些对话然后将产生的特征存储为DICOM SR。

**I want to customize my extraction. How do I do that?  我想自定义我的特征提取，我该如何做？**

也可参阅Customizing the Extraction。PyRadiomics可以通过多种方式进行自定义设置，但是最简单方式是提供一个参数配置文件。在这个yaml结构的文档中你可以自定义你的设置，激活的特征和影像类型。我们强烈推荐你使用这种方法进行自定义设置，因为他包含了所有设置在一个可读的文件中，我们可以将该文件分享给其它使用者，更重要的是在提取之前检查其合理性。


**Does PyRadiomics support voxel-wise feature extraction?  PyRadiomics支持体素特征提取么？**

支持，在2.0版本中，引入了voxelwise计算。但是，由于这需要为每一个体素进行计算，因此进行voxelwise提取会更慢，且由于结果是每一个特征组成的特征图谱，结果的尺寸也会更大。参阅usage部分以获取更多有关voxel-based提取的信息。


**How should the input file for pyradiomics in batch-mode be structured?  Batch-mode模式下pyradiomics的输入文件该如何组织？**

当前，pyradiomics的批量输入文件，是通过一个指定用来提取特征的image mask组合的csv文件构成的。该文件必须包含一个标头，至少包含“Image”和“Mask”（注意大小写）。这确保列中分别包含image和mask文件所在的位置。之后的每一行代表一个image和mask的组合。也可包含其它的列，会参照输入的顺序复制到结果中，计算的特征会作为其它列附在结尾。N.B. 所有标头名字应该是独一无二且与pyradiomics产生的任何标头（即特征）名字不相符的。


### 2.10.2 Common Errors  常见错误

**Error loading parameter file  错误载入参数配置文件**

当我尝试载入我自己的参数配置文件时，出现错误：”CoreError: Unable to load any data from source yaml file”

这是一个PyKwalify在无法读取参数配置文件时抛出的错误。最常见的原因是，当文件使用tabs缩进时，产生了“token (‘t’) not recognized error”错误。确保这些缩进使用2或4个空格。


**Geometry mismatch between image and mask  image和mask形状不匹配**

我的mask是基于另外一个比我输入的image文件更大的影像制作的，我还能提取特征么？

基于多种原因，当传递特征类时，image和mask需要具有相同的形状（i.e.相同的空间分辨率，大小，方向和原点）。为了达到这一目的，PyRadiomics在流程中进行了多项检查以确保这一目的达成。获取更多有关mask检查的信息，参见checkMask()。

如果形态学错误是由于原点，空间分辨率或方向上微小的差异构成的，你可以通过设置提高geometryTolerance容忍度（来调整）。如果错误比较大，或者维度不匹配，你需要将mask重采样至image的参考分辨率。一个和此有关的案例提供在bin\resampleMask.py文件内，并通过在PyRadiomics设置correctMask为True来使用，但该校正仅在一个mask中包含合理的ROI而形态不匹配时有效（i.e.mask包含的labe没有超过image的物理边界）。

**ValueError: （‘Label (. . . ) not present in mask. Choose from [. . . ]’**

这个错误意味着label标记的ROI不存在。I.e. 即在mask中不包含使用label值标记的volume。为了修正该错误，这个错误同样会列出找到的其它可供使用的label值。如果在这个错误最后没有列出任何值，说明在该mask中不存在分割。

Note：有一种可能，即在原始mask中存在体素分割，但是在重采样过程中丢失了（upsamping时）。在这种情况下，ROI对于resampledPixelSpacing的需求太小了因此被作为“不存在分割”。


**I’m unable to calculate texture matrices and getting a RunTimeError instead 我不能提取纹理特征矩阵并且遇到了RunTimeError**

这个错误意味着在使用C拓展计算矩阵时发生了错误。这里有几种可能的原因：

+ “Error parsing array arguments.”
这个错误发生在，提供给函数的Image或Mask不能解析为numpy array时。

+ “Expected image and mask to have equal number of dimensions.”
发生在提供的image和mask不具有同样的维度时。可以提取N维的特征，但是也需要image和mask在维度上具有相同的大小和数量。

+ “Dimensions of image and mask do not match.”
该错误意味着mask array和image array的大小不匹配。因为numpy arrays不包含向物理世界传递的信息，因此不同大小的array不能互相匹配。你可以在将其转换至相应的numpy array以进行特征计算之前，通过重采样simplITK-IMGAE mask对象至image的形状来解决该问题。也可参考Geometry mismatch between image and mask。

+ “Error parsing distances array.”
如果C拓展不能解析提供的距离参数，会出现该错误。在设置中，distances参数应该设置为元组或一系列值构成的列表。

+ “Expecting distances array to be 1-dimensional.”
提供的距离参数产生的另一个错误。设置的数列应该是1维的。（没有嵌套的数列）

+ “Error calculating angles.”
这个错误意味着，在根据提供的距离生成一个角度时出现了错误。当前，该错误仅发生在提供的distance<1时。

+ “Number of elements in <\Matrix> would overflow index variable! (. . . )”
这个错误发生在输出的（展平后的）array太大了，超过了最大的整数值（～2mln）。
该错误往往是由于离散后产生的bin分组太多，导致在离散后的image中用于纹理计算的灰度值范围太大了。我们同样建议采用一个bin width，使其离散后产生的bin分组不超过150-200。使用DEBUG级别的记录运行代码，以显示产生的bin分组的数目或许可以帮助指示你的矩阵有多大。

+ “Failed to initialize output array for <\Matrix>”
这个错误意味这电脑没有办法为输出分配内存。这个大多数是由于输出的尺寸太大了，或可供分配的内存太小了。与上述内容相同，可以使用DEBUG级别的记录运行代码，以查看产生的bins分组有多少（指示矩阵有多大）。

+ “Calculation of <\Matrix> Failed.”
这个错误意味着在计算矩阵本身是发生了错误。一般发生在代码试图在输出的array中设置一个超出范围的元素时发生。这可能发生在通过PYTHON调用C函数时，ROI中体素的灰度值大于给定的Ng参数。


**I’m able to extract features, but many are NaN, 0 or 1. What happened?  我可以提取特征，但很多值是NaN，0，1，发生了什么？**

可能是因为分割太小了没办法提取一个合理的纹理。检查VoxelNum值，即输出结果中的附加信息。这代表经预处理后ROI中体素的数量，是用于特征计算的体素的数目。

另外一种可能是离散化后产生的灰度值太多或太少。你可以利用给定的binwidth参数检查ROI中的灰度值的范围（first order feature）。更多的bins分组可以捕捉更多灰度值上的差异，但是过多的bins分组（与voxels的数目相比）会导致低概率出现在纹理矩阵中，会产生无意义的特征。关于灰度值离散的数量，没有一个理想的答案，根据模态不同答案亦不相同。有研究指出PET的bins分组在16-128之间时，纹理特征没有显著差异。


**I’m missing features from my output. How can I see what went wrong?  结果中由遗漏的特征，我该如何查看发生了什么？**

如果某一特征计算或滤波处理失败，会记录一个警告。如果你想知道到底在工具箱中发生了什么，pyradiomics提供拓展功能的debug记录。你可以通过激活他以输出其中的内容，或将其存储在一个分离的LOG记录文件中。输出由radiomics.setVerbosity() 控制，并且可以通过radiomics.logger接入PyRadiomics logger。也可参考这里，此外存储库中的案例展示了如何设置logging。


**Radiomics module not found in jupyter notebook  Jupyter notebook里找不到Radiomics模块**

我安装了PyRadiomics，但是当我运行jupyter notebbook时，我遇到ImportError: No module named radiomics。

这里可能有两种原因：

1. 当通过存储库安装PyRadiomics时，你的Python路径变量会更新以使python可以找到该软件包。但是，这个值仅在其重启时在命令行窗口中更新。如果你的jupyter notebook在安装过程正在运行，你需要重启它。

2. 在你的机器中可以同时安装多个版本的Python。确保pyradiomics安装在和你的jupyter notebook同一个版本的Python中。


### 2.10.3 Building PyRadiomics from source  从源安装PyRadiomics

**During setup, python is unable to compile the C extensions.  安装期间，python无法编译C拓展。**

这个可以发生在python没有编译器可以获取时。如果你是在windows中进行安装，可以在[此处](https://wiki.python.org/moin/WindowsCompilers)找到免费的编译器。


**Error loading C extensions.  错误载入C拓展。**

当我尝试运行pyradiomics时，遇到Error loading C extensions

当pyradiomics安装时，C拓展经编译并复制到安装文件夹中，默认为site-packages文件夹。然而当从存储库运行笔记本时，pyradiomics有可能直接运行源代码（i.e.在开发者模式下运行）。你可以使用radiomics.__path__检查，当在开发者模式下运行是[’radiomics’]，在开发者模式下在安装的文件夹下运行是[\'path/to/python/Lib/site-packages’]。如果是在开发者模式下运行，默认情况下无法获取C拓展。为了使在开发者模式下可以获取，在命令行中运行python setup.py build_ext --inplace，与运行install命令相似，但是仅编译C拓展并将其复制到源文件夹中（使它们在从source tree运行时可用）。

### 2.10.4 Miscellaneous  其他内容
**Which python versions is PyRadiomics compatible with?  PyRadiomics兼容哪些Python版本？**

PyRadiomics与Python3版本兼容。在PyRadiomics 3.0版本中尽管还保留了兼容的代码，已经与Python2版本不兼容了。而自动化检测功能仅支持在python versions 3.5, 3.6 and 3.7 (64 bits architecture)使用。在Python < 2.6的版本中均不支持。其它Python版本也可能与PyRadiomics兼容，但是没有经过测试因此也不保证可以工作。Pre-built wheels仅支持python的测试版本(3.5, 3.6 and 3.7)


**A new version of PyRadiomics is available! Where can I find out what changed? 新版本的PyRadiomics发布了，我在哪里可以看到改变了什么？**

当一个新版本发布时，会在release statement发布一个更新日志。在发布中间，变化不会详细的用文档说明，但是所有的变化都是使用Pull requests进行的。检查merged pull request查看最新的变化。


**I have some ideas for PyRadiomics. How can I contribute?  关于PyRadiomics我有一些新的想法，我该如何参与？**

我们欢迎对pyradiomics的建议和帮助。参考guidelines查看如何帮助PyRadiomics。PyRadiomics使用的签署方式和代码格式的文档说明在Developers模块中。


**I found a bug! Where do I report it?  我发现了一个bug，我该如何报告它？**

在将每一个新的附件并入稳定的版本时我们都会进行测试，以尽可能保持PyRadiomics没有bug。但是，没有任何事情是完美的，还是有可能存在一些bug。在GitHub中通过opening an issue报告你遇到的bug。如果你想帮助修复它，我们欢迎你使用你的补丁建立一个pull request。


**My question is not listed here. . .  这里没有我的问题**

如果这里没有列出你的问题，参考[pyradiomics forum on 3D Slicer discourse](https://discourse.slicer.org/c/community/radiomics/23) 或  [issues on GitHub](https://github.com/AIM-Harvard/pyradiomics/issues)。免费提出疑问或问题我们会尽快的回复你。

