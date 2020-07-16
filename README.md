# ViewFaceCore
- 超简单的人脸识别库 0.2
- C# 库
- Nuget Pack

# 更新
- 2020年7月16日: 新增活体检测方法

# 样例
[WinForm 摄像头人脸检测](https://github.com/View12138/ViewFaceCoreDemo)

# 使用

### 一、1 分钟在你的项目中集成人脸识别

#### 1. 创建你的 .NET 应用
  - .NET Standard >= 2.0
  - .NET Core >= 2.0
  - .NET Framework >= 4.6.1^2

#### 2. 使用 Nuget 安装 `ViewFaceCore`
  - Author : View
  - Version >= 0.1.1
  > 此 Nuget 包会自动添加依赖的 C++ 库，以及最精简的识别模型。  
  > 如果需要其它场景的识别模型，请下载 [SeetaFace6 模型文件](https://github.com/seetafaceengine/SeetaFace6#%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98)。  

#### 3. 在项目中编写你的代码
  - 一个简单的例子 `ViewFaceTest/Program.cs`

### 二、说明

**`ViewFaceCore.Sharp.ViewFace`** : 人脸识别类

#### 1. 属性说明
| 属性名称 | 类型 | 说明 | 默认值 |
| - | - | - | - |
| `ModelPath` | `string` | 获取或设置模型路径 [ 如非必要，请勿修改 ] | `./model/` |
| `FaceType` | `FaceType` | 获取或设置人脸类型 | `FaceType.Light` |
| `MarkType` | `MarkType` | 获取或设置人脸关键点类型 | `MarkType.Light` |
| `DetectorSetting` | `DetectorSetting` | 获取或设置人脸检测器设置 | `new DetectorSetting()` |
  
#### 2. 方法说明
```

using System.Drawing;
using ViewFaceCore.Sharp;
using ViewFaceCore.Sharp.Model;

// 识别 bitmap 中的人脸，并返回人脸的信息。
FaceInfo[] FaceDetector(Bitmap);

// 识别 bitmap 中指定的人脸信息 info 的关键点坐标。
FaceMarkPoint[] FaceMark(Bitmap, FaceInfo);

// 提取人脸特征值。
float[] Extract(Bitmap, FaceMarkPoint[]);

// 计算特征值相似度。
float Similarity(float[], float[]);

// 判断相似度是否为同一个人。
bool IsSelf(float);

// 单帧 活体检测
public AntiSpoofingStatus AntiSpoofing(Bitmap bitmap, FaceInfo info, FaceMarkPoint[] points, bool global);

// 视频帧 活体检测
public AntiSpoofingStatus AntiSpoofingVideo(Bitmap bitmap, FaceInfo info, FaceMarkPoint[] points, bool global);

```

也可以引用 `ViewFaceCore.Sharp.Extends` 命名空间，使用扩展方法进行活体检测

```
// 使用视频帧的 Bitmap 数组进行活体检测
public static AntiSpoofingStatus AntiSpoofingVideo(Bitmap[] bitmaps, int faceIndex, bool global)
```

# 说明

| 项目 | 语言 | 说明 |
| - | - | - |
| ViewFace | `C++` | 基于 `SeetaFace6` 的接口封装，支持 x86、x64 |
| ViewFaceCore | `C#` | 基于 `ViewFace` 的 C# 形势的封装，支持 AnyCPU |
| ViewFaceTest | `C#` | 调用 `ViewFaceCore` 实现的简单的图片人脸识别 |

# 编译
- 开发工具 : Visual Studio 2019 16.5.5
- 构建平台 : Windows 10 专业版 2004 19041.329

### `ViewFace` 项目
- 下载 [SeetaFace6 开发包](https://github.com/seetafaceengine/SeetaFace6#%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98)
- 设置 不同的平台 [x86、x64] 下的相关依赖路径，链接路径，生成路径
- 分别编译并得到 不同平台的 `ViewFace.dll`

### `ViewFaceCore` 项目
- 直接编译生成 AnyCPU 的 `ViewFaceCore.dll` 
- 将下载的 `模型文件` 拷贝至 `model` 文件夹中
- 在 .NET 项目中引用 `ViewFaceCore.dll` 即可
