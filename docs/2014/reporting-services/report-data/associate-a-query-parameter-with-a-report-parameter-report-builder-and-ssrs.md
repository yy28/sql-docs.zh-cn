---
title: 将查询参数与报表参数相关联（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- queries [Reporting Services], parameters
- parameters [Reporting Services], queries
ms.assetid: 6d297e1a-ff71-472a-addc-349e863092b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 697a8bbfa77a8afcabfdf00deef93620ff607233
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107467"
---
# <a name="associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs"></a>将查询参数与报表参数相关联（报表生成器和 SSRS）
  在您定义包含查询变量的数据集查询时，将对查询命令进行分析。 对于每个查询变量，都会创建相应的数据集参数和报表参数。 数据集参数将指向报表参数。 这样可以使用户输入一个直接传递给查询的值。 每次您编辑查询命令时，都会发生相同的过程。  
  
 如果重命名绑定到查询参数的报表参数，则需要使用本主题中的过程手动将查询参数链接到重命名的报表参数。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-query-parameter-with-a-report-parameter"></a>将查询参数与报表参数相关联  
  
1.  在“报表数据”窗格中，右键单击数据集，再单击“数据集属性”，然后单击“参数”。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”菜单上的“报表数据”。  
  
2.  在 **“参数名称”** 列中，查找查询参数的名称。 将基于查询自动填充参数名称。 每次更改查询时，都会检查查询是否有新的查询参数。 手动创建的查询参数不会随着查询的更改而变化。  
  
    -   在 **“参数名称”** 中，查找查询中存在的查询参数名称。 还可以手动添加新的查询参数，并输入名称。  
  
    -   在 **“参数值”** 中，键入或选择计算结果为要传递给查询参数的值的表达式。 这通常为报表参数的名称。  
  
        > [!NOTE]  
        >  您不仅可以将报表参数作为查询参数的值。 也可以使用任何表达式来计算参数值。  
  
3.  对于其他查询参数，重复执行步骤 2。  
  
## <a name="see-also"></a>请参阅  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [报表参数概念&#40;报表生成器和 SSRS&#41;](../report-design/report-parameters-concepts-report-builder-and-ssrs.md)  
  
  
