---
title: 添加背景图像（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df5de06ef60cf22a023589efb9d67f0f521f1c40
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032688"
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>添加背景图像（报表生成器和 SSRS）
  您可以向报表项（如矩形、文本框、列表、矩阵、表和某些图表部件）或报表区域（如页眉、页脚或表体）添加背景图像。 在“属性”窗格中，可以为报表设计图面上显示 **BackgroundImage** 的任何所选项定义背景图像。 与其他图像相似，背景图像可以是指向报表服务器上的图像的 URL、数据集字段的图像，也可以是报表定义中嵌入的图像。 若要使用在报表中嵌入的图像，您必须首先向报表定义中添加该嵌入图像，然后才能向设计图面中添加该图像。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>在报表定义中嵌入图像  
  
1.  在“报表数据”窗格中，右键单击“图像”节点，然后单击“添加图像”。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”选项卡上的“报表数据”。  
  
2.  导航到您要在报表定义中嵌入的图像，然后单击 **“确定”**。  
  
### <a name="to-add-a-background-image"></a>添加背景图像  
  
1.  在报表设计视图中，选择要向其添加背景图像的报表项。  
  
2.  如果“属性”窗格不可见，请在 **“视图”** 选项卡上选择 **“属性”**。  
  
3.  在“属性”窗口中，展开 **BackgroundImage**，然后执行以下操作：  
  
    -   对于嵌入的图像：  
  
         将 **“源”** 设置为 **“嵌入”**。  
  
         将 **“值”** 设置为在报表中嵌入的图像的名称。  
  
    -   对于外部图像：  
  
         将 **“源”** 设置为 **“外部”**。  
  
         将 **“值”** 设置为指向图像的有效路径。 此图像可在本机模式或 SharePoint 集成模式下处于报表服务器上，或者可处于任何其他网站上。 有关详细信息，请参阅[添加外部图像（报表生成器和 SSRS）](add-an-external-image-report-builder-and-ssrs.md)。  
  
    -   对于包含在报表项所连接的数据库的某个字段中的图像：  
  
         将 **“源”** 设置为 **“数据库”**。  
  
         将 **“值”** 设置为报表数据集中某个字段的名称。 有关详细信息，请参阅[添加数据绑定图像（报表生成器和 SSRS）](add-a-data-bound-image-report-builder-and-ssrs.md)。  
  
         对于 MIMEType 或文件格式，为图像选择适当的 MIME 类型，如 .bmp。  
  
        > [!NOTE]  
        >  仅当 **Source** 属性设置为 **Database**时，MIMEType 才适用。 如果将 **Source** 属性设置为 **External** 或 **Embedded**，则忽略 **MIMEType** 的值。  
  
    -   对于 **BackgroundRepeat**，选择一个表达式，再选择 **Default**、 **Repeat**、 **RepeatX**、 **RepeatY**或 **Clip**。  
  
         对于图表中的背景图像， **BackgroundRepeat** 可设置为 **Default**、 **Repeat**、 **Fit**和 **Clip**，但不可设置为 **RepeatX** 或 **RepeatY**。  
  
## <a name="see-also"></a>请参阅  
 [图像（报表生成器和 SSRS）](images-report-builder-and-ssrs.md)   
 [“图像属性”对话框 ->“常规”（报表生成器和 SSRS）](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
