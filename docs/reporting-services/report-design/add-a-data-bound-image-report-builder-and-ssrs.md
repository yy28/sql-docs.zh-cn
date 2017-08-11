---
title: "添加数据绑定图像 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 253d3abfffae056d6300e2203623e7af023a2476
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>添加数据绑定图像（报表生成器和 SSRS）
  报表可以包括对存储在数据库中的图像的引用。 此类图像称为“数据绑定图像”。 例如，在产品列表中产品名称旁边显示的图片就是数据绑定图像。  
  
 将数据绑定图像添加到页眉或页脚还需要其他步骤。 有关详细信息，请参阅[页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>添加数据绑定图像  
  
1.  在报表设计视图中，创建一个表和一个数据集，表中具有数据源连接，数据集中具有包含二进制图像数据的一个字段。 有关详细信息，请参阅[表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)。  
  
2.  在您的表中插入列。 有关详细信息，请参阅[插入或删除列（报表生成器和 SSRS）](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **“插入”** 菜单上，单击 **“图像”**，然后在新列的数据行中单击。  
  
4.  在 **“图像属性”** 对话框的“常规”页上，在 **“名称”** 文本框中键入名称，或接受默认名称。  
  
5.  （可选）在“工具提示”文本框中，键入当用户将鼠标指针悬停在以 HTML 格式呈现的报表中的图像上时所要显示的文本。  
  
6.  在 **“选择图像源”**中，选择 **“数据库”**。  
  
7.  在 **“使用此字段”**中，选择在您的报表中包含图像的字段。  
  
8.  在 **“使用此 MIME 类型”**中，选择图像的 MIME 类型或文件格式，如 bmp。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在报表设计图面上将出现图像占位符。  
  
## <a name="see-also"></a>另请参阅  
 [映像 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [在报表 &#40; 中嵌入图像报表生成器和 SSRS &#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [添加外部图像 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [映像属性对话框中，常规 &#40;报表生成器和 SSRS &#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
