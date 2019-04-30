---
title: 添加数据绑定图像（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 162be037a4ae458fdc609b76d8cad1ee21c27e0b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206975"
---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>添加数据绑定图像（报表生成器和 SSRS）
  报表可以包括对存储在数据库中的图像的引用。 此类图像称为“数据绑定图像”。 例如，在产品列表中产品名称旁边显示的图片就是数据绑定图像。  
  
 将数据绑定图像添加到页眉或页脚还需要其他步骤。 有关详细信息，请参阅[页眉和页脚（报表生成器和 SSRS）](page-headers-and-footers-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>添加数据绑定图像  
  
1.  在报表设计视图中，创建一个表和一个数据集，表中具有数据源连接，数据集中具有包含二进制图像数据的一个字段。 有关详细信息，请参阅[表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)。  
  
2.  在您的表中插入列。 有关详细信息，请参阅[插入或删除列（报表生成器和 SSRS）](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **“插入”** 菜单上，单击 **“图像”**，然后在新列的数据行中单击。  
  
4.  在 **“图像属性”** 对话框的“常规”页上，在 **“名称”** 文本框中键入名称，或接受默认名称。  
  
5.  （可选）在“工具提示”文本框中，键入当用户将鼠标指针悬停在以 HTML 格式呈现的报表中的图像上时所要显示的文本。  
  
6.  在 **“选择图像源”** 中，选择 **“数据库”**。  
  
7.  在 **“使用此字段”** 中，选择在您的报表中包含图像的字段。  
  
8.  在“使用此 MIME 类型”中，选择图像的 MIME 类型或文件格式，如 bmp。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在报表设计图面上将出现图像占位符。  
  
## <a name="see-also"></a>请参阅  
 [图像（报表生成器和 SSRS）](images-report-builder-and-ssrs.md)   
 [在报表中嵌入图像（报表生成器和 SSRS）](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [添加外部图像（报表生成器和 SSRS）](add-an-external-image-report-builder-and-ssrs.md)   
 [“图像属性”对话框 ->“常规”（报表生成器和 SSRS）](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
