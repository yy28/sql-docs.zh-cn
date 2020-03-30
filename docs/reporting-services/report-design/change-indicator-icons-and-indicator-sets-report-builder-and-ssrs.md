---
title: 更改指示器图标和指示器集（报表生成器）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8a056adf-4473-473d-9b0c-314675af7bfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b93ba65ddda79ef44585c748ee2c465c1b9a25f2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081856"
---
# <a name="change-indicator-icons-and-indicator-sets-report-builder-and-ssrs"></a>更改指示器图标和指示器集（报表生成器和 SSRS）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 为分页报表提供的预先配置指示器集并非总是能够高效地描绘你的数据以及适合于传递的报表。 本主题提供的过程介绍如何更改指示器图标的外观，以及如何更改指示器集以便包括不同的指示器图标或者更多或更少的指示器图标。  
  
 可以通过使用表达式设置颜色之类的选项。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
## <a name="to-change-the-color-of-an-indicator-icon"></a>更改指示器图标的颜色  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”  。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  单击您要更改的图标旁的 **“颜色”** 列中的向下箭头，单击要使用的颜色、 **“无颜色”** 或 **“其他颜色”** 。  
  
     根据需要，可以单击“表达式”(fx) 按钮以编辑设置该“颜色”选项的值的表达式    。  
  
     如果您单击了 **“其他颜色”** ，则 **“选择颜色”** 对话框将打开，从中可以选择多种不同的颜色。 有关其选项的详细信息，请参阅[选择颜色对话框（报表生成器和 SSRS）](https://msdn.microsoft.com/library/ac7089a3-5c7b-4f53-8348-180610e86da2)。 单击 **“确定”** 关闭 **“选择颜色”** 对话框。  
  
4.  单击“确定”。   
  
## <a name="to-change-the-icon"></a>更改图标  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”  。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  单击您要更改的图标旁的向下箭头，然后选择其他图标。  
  
     根据需要，可以单击“表达式”(fx) 按钮以编辑设置该“图标”选项的值的表达式    。  
  
4.  单击“确定”。   
  
## <a name="to-use-a-custom-image-as-an-indicator-icon"></a>使用自定义图像作为指示器图标  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”  。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  单击您要更改的图标旁的向下箭头，然后选择 **“图像”** 。  
  
4.  在 **“选择图像源”** 列表中，单击 **“外部”** 、 **“嵌入”** 或 **“数据库”** 。  
  
5.  根据图像的源，执行以下操作之一：  
  
    -   若要使用在报表外部存储的图像，请单击 **“浏览”** 并且找到该图像。 该报表将包含对图像的引用。  
  
    -   若要使用在报表中嵌入的图像，请单击 **“导入”** 并且找到该图像。 图像将被添加到报表定义中并一起保存。  
  
    -   若要使用位于数据库中的图像，请在 **“使用此字段”** 列表中选择相应字段， 然后在 **“使用此 MIME 类型”** 列表中选择图像的 MIME 类型。  
  
6.  单击“确定”。   
  
## <a name="to-add-an-icon-to-the-indicator-set"></a>将图标添加到指示器集  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”  。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  单击“添加”  。 将添加一个指示器，并且使用默认图标和 **“无颜色”** 选项。  
  
     配置该指示器以便使用您所需的图标和颜色。 本主题中前面的过程描述用于执行此操作的步骤。  
  
4.  单击“确定”。   
  
## <a name="to-delete-an-icon-to-the-indicator-set"></a>从指示器集中删除图标  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”  。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  选择要删除的图标，然后单击 **“删除”** 。  
  
4.  单击“确定”。   
  
## <a name="see-also"></a>另请参阅  
 [指示器（报表生成器和 SSRS）](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
