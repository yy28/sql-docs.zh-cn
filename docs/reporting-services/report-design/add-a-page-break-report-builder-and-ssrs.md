---
title: 添加分页符（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3846cd48-2787-47e9-b13b-7fc45a205f68
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca618e82e9eed6a0cb43582b8aa1feff33d67626
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65574805"
---
# <a name="add-a-page-break-report-builder-and-ssrs"></a>添加分页符（报表生成器和 SSRS）
  您可以向数据区域内的矩形、数据区域或组添加分页符，以控制每个页面中的信息量。 添加分页符能够提高已发布报表的性能，因为在您查看报表时，系统只需处理每个页面中的项。 如果整个报表位于一个页面中，则您只能在所有项都得到处理后才能查看报表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-break-to-a-data-region"></a>向数据区域添加分页符  
  
1.  在设计图面上，右键单击数据区域的角部图柄，然后单击“Tablix 属性”  。  
  
2.  在 **“常规”** 选项卡中的 **“分页符选项”** 下选择下列选项之一：  
  
    -   **在以下项前面添加分页符**。 当您希望在表前面添加分页符时可选择此选项。  
  
    -   **在以下项后面添加分页符**。 当您希望在表后面添加分页符时可选择此选项。  
  
    -   **如有可能，调整表的大小以显示在同一页上**。 当您希望将数据保留在同一页面时可选择此选项。  
  
### <a name="to-add-a-page-break-to-a-rectangle"></a>向矩形添加分页符  
  
1.  在设计图面上，右键单击要在其中添加分页符的矩形，然后单击“矩形属性”  。  
  
2.  在 **“常规”** 选项卡中的 **“分页符选项”** 下选择下列选项之一：  
  
    -   **在以下项前面添加分页符**。 当您希望在矩形前面添加分页符时可选择此选项。  
  
    -   **在以下项后面添加分页符**。 当您希望在矩形后面添加分页符时可选择此选项。  
  
    -   **去掉分页符上的边框**。 当您希望分页符不带边框时可选择此选项。  
  
    -   **如有可能，将内容显示在一页中**。 当您希望将矩形中的内容保留在同一页面时可选择此选项。  
  
### <a name="to-add-a-page-break-to-a-row-group-in-a-table-matrix-or-list"></a>将分页符添加到表、矩阵或列表中的行组  
  
1.  在“分组”窗格中，右键单击行组，然后单击“组属性”  。  
  
    > [!NOTE]  
    >  将忽略列组上的分页符。  
  
2.  在 **“分页符”** 选项卡中，选择 **“在组的每个实例之间”** ，以便在表中组的每个实例之间添加一个分页符。  
  
3.  此外，还可以选择 **“同样在组的开头”** 或 **“同样在组的结尾”** ，指定为组在表中的开始位置或结束位置添加分页符。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
  
  
