---
title: 使用脚本任务处理图像 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4529ded6049327261ac92a76cc9861b7cec7dd61
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204577"
---
# <a name="working-with-images-with-the-script-task"></a>使用脚本任务处理图像
  除文本和数值数据外，产品数据库或用户数据库还经常包含图像。 Microsoft .NET Framework 中的 `System.Drawing` 命名空间提供用于操作图像的类。  
  
 [示例 1：将图像转换为 JPEG 格式](#example1)  
  
 [示例 2：创建并保存缩略图图像](#example2)  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
##  <a name="example1"></a>示例 1 说明：将图像转换为 JPEG 格式  
 下面的示例打开一个由变量指定的图像文件，并使用编码器将其保存为压缩后的 JPEG 文件。 检索编码器信息的代码封装在一个私有函数中。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>将此脚本任务示例配置为用于单个图像文件  
  
1.  创建一个名为 `CurrentImageFile` 的字符串变量，并将其值设置为一个现有图像文件的路径和名称。  
  
2.  上**脚本**页**脚本任务编辑器**，将添加`CurrentImageFile`变量`ReadOnlyVariables`属性。  
  
3.  在脚本项目中，设置一个对 `System.Drawing` 命名空间的引用。  
  
4.  在您的代码中，使用 `Imports` 语句导入 `System.Drawing` 和 `System.IO` 命名空间。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>将此脚本任务示例配置为用于多个图像文件  
  
1.  将脚本任务放入 Foreach 循环容器。  
  
2.  在“Foreach 循环编辑器”的“集合”页中，选择“Foreach 文件枚举器”作为枚举器，并指定源文件的路径和文件掩码，如“*.bmp”。  
  
3.  在“变量映射”页中，将 `CurrentImageFile` 变量映射到索引 0。 此变量在枚举器的每次迭代中将当前文件名传递给脚本任务。  
  
    > [!NOTE]  
    >  这些步骤是在执行用于单个图像文件配置过程中列出的步骤之外还要执行的步骤。  
  
### <a name="example-1-code"></a>示例 1 代码  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a>示例 2 说明：创建并保存缩略图图像  
 下面的示例打开一个由变量指定的图像文件，在保持宽高比不变的情况下创建一个该图像的缩略图，并将此缩略图以修改后的名称保存。 在保持宽高比不变的情况下计算缩略图的高度和宽度的代码封装在一个私有子例程中。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>将此脚本任务示例配置为用于单个图像文件  
  
1.  创建一个名为 `CurrentImageFile` 的字符串变量，并将其值设置为一个现有图像文件的路径和名称。  
  
2.  再创建整数变量 `MaxThumbSize`，并赋值（单位为像素），例如 100。  
  
3.  上**脚本**页**脚本任务编辑器**，将添加到这两个变量`ReadOnlyVariables`属性。  
  
4.  在脚本项目中，设置一个对 `System.Drawing` 命名空间的引用。  
  
5.  在您的代码中，使用 `Imports` 语句导入 `System.Drawing` 和 `System.IO` 命名空间。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>将此脚本任务示例配置为用于多个图像文件  
  
1.  将脚本任务放入 Foreach 循环容器。  
  
2.  在“Foreach 循环编辑器”的“集合”页中，选择“Foreach 文件枚举器”作为“枚举器”，并指定源文件的路径和文件掩码，如“*.jpg”。  
  
3.  在“变量映射”页中，将 `CurrentImageFile` 变量映射到索引 0。 此变量在枚举器的每次迭代中将当前文件名传递给脚本任务。  
  
    > [!NOTE]  
    >  这些步骤是在执行用于单个图像文件配置过程中列出的步骤之外还要执行的步骤。  
  
### <a name="example-2-code"></a>示例 2 代码  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
