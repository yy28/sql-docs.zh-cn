---
title: 在报表中嵌入图像（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b1541073379aa27c932fcadf7558de7d34c57e8d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59938863"
---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>在报表中嵌入图像（报表生成器和 SSRS）
  报表中可以包含嵌入图像。 嵌入图像可确保图像对报表始终可用，但会影响报表定义（即定义报表的文件）的大小。 报表中嵌入的图像在“报表数据”窗格中列出。  
  
 您最好将某一图像嵌入到报表定义中，然后将该图像添加到设计图面。 有关详细信息，请参阅[添加背景图像（报表生成器和 SSRS）](add-a-background-image-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>在报表中嵌入图像  
  
1.  在报表设计视图的 **“插入”** 选项卡上，单击 **“图像”**。  
  
2.  在设计图面上，单击某个位置，然后拖动一个框调整到所需图像大小。  
  
3.  在 **“图像属性”** 对话框的 **“常规”** 页中，在 **“名称”** 文本框中键入名称，或接受默认名称。  
  
4.  （可选）在“工具提示”文本框中，键入当用户将鼠标指针悬停在呈现报表中的图像上时所要显示的文本。  
  
5.  在 **“选择图像源”** 中，选择 **“嵌入”**。  
  
6.  单击 **“使用此图像”** 文本框旁的 **“导入”** 按钮。  
  
7.  在 **“文件类型”** 中，选择图像文件类型，导航到该文件，然后单击 **“打开”**。  
  
8.  在 **“图像属性”** 对话框中，单击 **“确定”**。  
  
     图像将显示在您在设计图面上绘制的框中，并且文件显示在“报表数据”窗格中“图像”文件夹的下方。  
  
    > [!NOTE]  
    >  MIME 类型（如 bmp）是导入图像时自动派生得来的。 若要更改 MIME 类型，请参见下一个过程。  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>（可选）更改导入图像的 MIME 类型  
  
1.  在“设计”视图中打开报表。  
  
2.  在设计图面上选择图像。 **“属性”** 窗格将显示图像属性。  
  
    > [!NOTE]  
    >  如果“属性”窗格不可见，请单击“视图”选项卡上的“属性”。  
  
3.  在 **MIMEType** 属性旁边的文本框内单击，并从下拉列表中选择一个新 MIME 类型。  
  
## <a name="see-also"></a>请参阅  
 [图像（报表生成器和 SSRS）](images-report-builder-and-ssrs.md)   
 [添加数据绑定图像（报表生成器和 SSRS）](add-a-data-bound-image-report-builder-and-ssrs.md)   
 [“图像属性”对话框 ->“常规”（报表生成器和 SSRS）](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
