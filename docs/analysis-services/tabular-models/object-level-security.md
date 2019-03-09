---
title: Analysis Services 表格模型对象级安全性 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d354aa64e8b6a1e98941011c30550a056f4c01c9
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685573"
---
# <a name="object-level-security"></a>对象级安全性
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
数据模型安全性以有效地实施开头[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)和行级筛选器来定义数据模型对象和数据的用户权限。 从表格 1400年模型开始，您还可以定义对象级安全性，包括表级别安全性和中的列级安全性[角色对象](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)。

## <a name="table-level-security"></a>表级别安全性

具有表级安全性，可以不只限于访问表数据，但也敏感的表名，从而帮助防止恶意用户发现如果表存在。 

 表级安全性设置的基于 JSON 的元数据中 Model.bim[表格模型脚本语言 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)，或[表格对象模型 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)。 设置**metadataPermission**的属性**tablePermissions**类[角色对象](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)到**无**。

在此示例中，Product 表 tablePermissions 类的 metadataPermission 属性设置为无:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Product",
        "metadataPermission": "none"
      }
    ]
  }
```

## <a name="column-level-security"></a>列级安全性

类似于表级别安全性，具有列级安全性，可以不只限于访问列数据，但还敏感列名称，帮助防止恶意用户发现某一列。

 列级安全性设置的基于 JSON 的元数据中 Model.bim[表格模型脚本语言 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)，或[表格对象模型 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)。 设置**metadataPermission**的属性**columnPermissions**类[角色对象](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)到**无**。

在此示例中，雇员表中的基准费率列的 columnPermissions 类的 metadataPermission 属性设置为无:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Employee",
        "columnPermissions": [
          {
            "name": "Base Rate",
            "metadataPermission": "none"
          }
        ]
      }
    ]
  }
```

## <a name="restrictions"></a>限制

*  如果这会破坏关系链，无法为模型中设置表级别安全性。 在设计时生成错误。
 例如，如果表 A 和 B 和 B 和 C 之间没有关系，则不能保护表 B。如果表 B 安全的对一个表的查询不能传输表 A 和 B 和 B 和 C 之间的关系无法在这种情况下，表 A 和 b。 之间配置单独的关系

    ![表级别安全性](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  因为它可能会无意中访问引入到受保护数据，不能从不同的角色组合行级安全性和对象级安全性。 在这种组合的角色的成员的用户的查询时生成错误。

*  如果它们引用的受保护的表或列，动态计算 （度量值、 Kpi、 DetailRows） 会自动受到限制。 尽管没有任何机制来显式安全度量值，则可以隐式安全更新来指代的受保护的表或列的表达式的度量值。

*  引用的受保护的列的关系的工作提供的表中的列是不安全。




## <a name="see-also"></a>请参阅  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Roles 对象 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)  
[表格模型脚本语言 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)  
[表格对象模型 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)。

  
