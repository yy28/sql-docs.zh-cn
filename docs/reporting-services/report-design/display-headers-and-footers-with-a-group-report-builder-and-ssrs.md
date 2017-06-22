---
title: "显示标头和组尾与组 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 22c9592550b79fa5fa25e31f023a6d53c5b002f5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>与组一起显示组头和组尾（报表生成器和 SSRS）
  您可以帮助控制是否在显示与 Tablix 数据区域中某个组相关联的动态行的同时显示静态行，如组头或组尾。  
  
 若要在多个页上重复所有列标题或行标题，可以设置 Tablix 数据区域的属性。 有关详细信息，请参阅 [在多个页中显示行标题和列标题（报表生成器和 SSRS）](https://msdn.microsoft.com/library/dd207045.aspx)。  
  
 若要控制与嵌套组相关联的动态行和列的呈现行为，或者与标签或小计相关联的静态行和列的呈现行为，必须设置 Tablix 成员的属性。 一个 Tablix 成员表示一个静态或动态的行或列。 每个静态成员重复一次。 例如，总计行就是一个静态行。 一个动态成员针对每个组实例重复一次。 例如，一个与具有组表达式 [Territory] 的组相关联的行针对每个唯一地区值重复一次。 有关 Tablix 成员的详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 可以在“分组”窗格中选择 Tablix 成员，并在“属性”窗格中设置 **KeepWithGroup**、 **KeepTogether**和 **RepeatOnNewPage** 属性。 使用 **KeepWithGroup** 可帮助将组头和组尾与组显示在相同页上。 使用 **KeepTogether** 可帮助将静态成员与组的行或列显示在一起。 使用 **RepeatOnNewPage** 可在以下页上重复显示组头和组尾：其中的每一页至少显示 **KeepWithGroup** 值所指定的行组成员的一个完整实例。 列组成员不支持**RepeatOnNewPage** 。  
  
> [!NOTE]  
>  **KeepWithGroup**、 **KeepTogether**和 **RepeatOnNewPage** 是可通过使用“分组”窗格的 **“高级模式”** 设置的组成员属性。 有关详细信息，请参阅[“分组”窗格（报表生成器）](../../reporting-services/report-design/grouping-pane-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>使静态行和一组与行组关联的动态行一起显示  
  
1.  在设计图面上，单击 Tablix 数据区域中的任意位置以将其选定。 “分组”窗格将显示数据区域的行组和列组。  
  
2.  在“分组”窗格的右侧，单击下箭头，然后单击 **“高级模式”**。 “行组”窗格显示行组层次结构的分层静态和动态成员。  
  
3.  单击要与组行一起显示的组头或组尾行所对应的静态成员。 “属性”窗格显示 **“Tablix 成员”** 属性。  
  
4.  在“属性”窗格中，单击 **KeepWithGroup**，然后从下拉列表选择以下值之一：  
  
    -   **无** 选择该选项表示没有指定使该成员与所选行组成员一起显示的首选项。  
  
    -   **前面** 选择该选项可以使该成员与上一组的成员一起显示。 您可能会对组尾行使用此值。  
  
    -   **后面** 选择该选项可以使该成员与下一组的成员一起显示。 您可能会对组头行使用此值。  
  
5.  （可选）预览报表。 如果可能，报表呈现器使该成员与指定行组成员一起显示。  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>使静态列和一组与列组关联的动态列一起显示  
  
1.  在设计图面上，单击 Tablix 数据区域中的任意位置以将其选定。 “分组”窗格将显示数据区域的行组和列组。  
  
2.  在“分组”窗格的右侧，单击下箭头，然后单击 **“高级模式”**。 “列组”窗格显示列组层次结构的分层静态和动态成员。  
  
3.  单击要与组列一起显示的静态列所对应的静态成员。 “属性”窗格显示 **“Tablix 成员”** 属性。  
  
4.  在“属性”窗格中，单击 **KeepWithGroup**，然后从下拉列表选择以下值之一：  
  
    -   **无** 选择该选项表示没有指定使该成员与所选列组成员一起显示的首选项。  
  
    -   **前面** 选择该选项可以使该成员与上一组的成员一起显示。 您可能会对在指定列组成员之前显示的列标签使用此值。  
  
    -   **后面** 选择该选项可以使该成员与下一组的成员一起显示。 您可能会对在指定列组成员之后显示的列总计使用此值。  
  
5.  （可选）预览报表。 如果可能，报表呈现器使该成员与指定列组成员一起显示。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](https://msdn.microsoft.com/library/dd220587.aspx)   
 
  
  
