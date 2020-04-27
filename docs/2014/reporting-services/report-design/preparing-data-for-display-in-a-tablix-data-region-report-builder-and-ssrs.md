---
title: 准备要在 Tablix 数据区域中显示的数据（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fbb00dc6-7887-480c-b771-cab6fecb8dcc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86418fd892c4f403f1e0207073a28e7933eb4b58
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105419"
---
# <a name="preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs"></a>准备要在 Tablix 数据区域中显示的数据（报表生成器和 SSRS）
  Tablix 数据区域显示来自数据集的数据。 您可以查看从数据集中检索的所有数据，也可以创建筛选器以便仅查看数据子集。 还可以添加条件表达式，以便填充 Null 值或修改对数据集的查询，使其包括定义现有列的排序顺序的列。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="working-with-nulls-and-blanks-in-field-values"></a>处理字段值中的 Null 值和空白  
 数据集中的字段集合的数据包含在运行时从数据源中检索到的所有值，包括 Null 值和空白。 通常 Null 值和空白是无法区分的。 在大多数情况下，这是所需行为。 例如， [Sum](report-builder-functions-sum-function.md) 和 [Avg](report-builder-functions-avg-function.md) 等数值聚合函数忽略 Null 值。 有关详细信息，请参阅 [聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)。  
  
 如果希望以不同方式处理 Null 值，则可以使用条件表达式或自定义代码替换 Null 值的自定义值。 例如，只要 `Null` 字段显示 Null 值，以下表达式则替换 `[Size]`文本。  
  
```  
=IIF(Fields!Size.Value IS NOTHING,"Null",Fields!Size.Value)  
```  
  
 有关在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据源检索数据之前在数据中消除 Null 值的详细信息，请参阅位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server 联机丛书 [上的](https://go.microsoft.com/fwlink/?linkid=120955)文档中的“Null 值”和“Null 值和联接”。  
  
## <a name="handling-null-field-names"></a>处理 Null 字段名称  
 只要查询结果集中存在 Null 字段自身，就可以在表达式中测试 Null 值。 使用自定义代码，可以测试在运行时从数据源返回的集合字段中是否存在字段自身。 有关详细信息，请参阅[数据集字段集合引用（报表生成器和 SSRS）](built-in-collections-dataset-fields-collection-references-report-builder.md)。  
  
## <a name="adding-a-sort-order-column"></a>添加排序顺序列  
 默认情况下，可以按字母顺序对数据集字段中的值排序。 若要按不同顺序排序，则可以在数据集中添加定义数据区域中的排序顺序的新列。 例如，若要对 `[Color]` 字段排序，并首先对白色和黑色项排序，则可以添加 `[ColorSortOrder]`列，如以下查询所示：  
  
```  
SELECT ProductID, p.Name, Color,  
   CASE  
      WHEN p.Color = 'White' THEN 1  
      WHEN p.Color = 'Black' THEN 2  
      WHEN p.Color = 'Blue' THEN 3  
      WHEN p.Color = 'Yellow' THEN 4  
      ELSE 5  
   END As ColorSortOrder  
FROM Production.Product p  
```  
  
 若要按照此排序顺序对表数据区域进行排序，请将详细信息组上的排序表达式设置为 `=Fields!ColorSortOrder.Value`。 有关详细信息，请参阅[对数据区域中的数据进行排序（报表生成器和 SSRS）](sort-data-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据集字段集合（报表生成器和 SSRS）](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
