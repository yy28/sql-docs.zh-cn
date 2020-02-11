---
title: 更改属性类型 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4406eb225002bbf5df93f8c67385694922d7d2c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482764"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>更改属性类型（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，数据类型或允许的字符数不正确时，管理员可以更改属性类型。  
  
 如果要更改属性类型以创建受限制列表（基于域的属性），请参阅[创建基于域的属性（用于 Excel 的 MDS 外接程序）](create-a-domain-based-attribute-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  不能更新“名称”**** 或“代码”**** 列的类型或长度。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域和 **“资源管理器”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../administrators-master-data-services.md)。  
  
-   必须存在现有的模型、实体和属性。  
  
### <a name="to-change-the-attribute-type"></a>更改属性类型  
  
1.  在 Excel 中，加载包含要更改的列（属性）的实体。 有关详细信息，请参阅将[数据从 MDS 加载到 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
2.  单击要更改的列中的任意单元。  
  
3.  在 **“生成模型”** 组中，单击 **“特性属性”**。  
  
4.  在 **“特性属性”** 对话框中，根据需要更新设置。  
  
5.  单击“确定”。   
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>在更改属性类型时会发生什么情况？  
 如果属性有任何依赖项，例如属性由任何 MDS 业务规则引用或属性包含在订阅视图中，则您更改属性的数据类型时，MDS 将：  
  
-   更改属性的数据类型。  
  
-   使用不包含任何值的后缀 "_old" 生成属性的副本。 这称为不**推荐使用**的属性。  
  
 但是，原始属性的所有现有依赖项将指向此不推荐使用的属性，而非指向已更改的属性。  
  
 这表示：  
  
-   您必须刷新业务规则才能指向已更改的属性，因为考虑到属性的新数据类型，逻辑可能会不一样。 您将必须编辑每个受影响的规则，然后重新处理说明删除不推荐使用的属性 (_old) 中的引用的表达式，以指向已更新的属性。  
  
-   你必须在 "集成管理" 选项下打开任何订阅视图，选择 "查看" 行，通过单击铅笔图标打开它进行编辑，然后单击 "**保存磁盘**" 图标以刷新视图定义。 重新生成视图语法不需要其他更改。  
  
-   包括该属性的临时表将向这些表添加一个不推荐使用的属性列，这意味着您的临时代码将受到影响。 要删除此不推荐使用的属性，您可以在更新业务规则和订阅视图后进行删除。  
  
 **删除不推荐使用的属性**  
  
 在删除任何不推荐使用的属性前，您必须删除对该属性的所有引用，例如修复业务规则和重新生成订阅视图（如前所述）。 否则，当您尝试删除不推荐使用的属性时，将在“系统管理”网页中收到错误，指示该属性因被某对象引用而无法删除。  
  
 若要删除属性，请参阅[删除属性 &#40;Master Data Services&#41;](../delete-an-attribute-master-data-services.md)  
  
> [!TIP]  
>  更改具有现有数据及相关实体的 MDS 属性的数据类型会很麻烦，特别是当存在依赖于实体的已声明的业务规则或订阅视图时。 最佳做法是从足够灵活可包含所需值的数据类型开始。 例如，字符串开始时可能会比较小，但是可能随着时间的推移需要延长，因此请考虑最坏的情况。 额外的文本字符串长度可能会成为负担（例如，宽 GUI 文本框很难适应屏幕），因此，请避免过长的字符串长度。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;Master Data Services&#41;](../attributes-master-data-services.md)   
 [构建模型 &#40;MDS Add-in for Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
