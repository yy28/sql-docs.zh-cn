---
title: "表格模型对象级别的安全性 |Microsoft 文档"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: 
ms.assetid: 
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bc44742d56d744e9d0d4c1f1697d0bcd4e40488c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="object-level-security"></a>对象级安全

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

数据模型安全性开头有效地实施[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)和行级筛选器，可以定义数据模型对象和数据的用户权限。 从表格 1400年模型开始，你还可以定义对象级安全，其中包括表级安全性和中的列级安全性[角色对象](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)。

## <a name="table-level-security"></a>表级别安全性

表级安全性，你可以不只限于访问表数据，但还敏感表名称，帮助防止恶意用户发现如果表存在。 

 在基于 JSON 的元数据在 Model.bim，设置表级安全性[表格模型脚本语言 (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)，或[表格对象模型 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)。 设置**metadataPermission**属性**tablePermissions**类[角色对象](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)到**无**。

在此示例中，Product 表 tablePermissions 类 metadataPermission 属性设置为无:

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

类似于表级安全性，使用列级安全你可以不仅限制对访问列数据，但还敏感列名称，帮助防止恶意用户发现某一列。

 列级安全性设置在基于 JSON 的元数据在 Model.bim，[表格模型脚本语言 (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)，或[表格对象模型 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)。 设置**metadataPermission**属性**columnPermissions**类[角色对象](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)到**无**。

在此示例中，雇员表中的基本速率列 columnPermissions 类 metadataPermission 属性设置为无:

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

*  无法为一个模型设置表级安全，如果其将中断关系链。 在设计时生成错误。
 例如，如果表 A 和 B 和 B 和 C 之间有关系，则不能保护表 b。如果表 B 提供保护，对一个表的查询不能传输表 A 和 B 和 B 和 C 之间的关系无法在这种情况下，表 A 和 b。 之间配置单独的关系

    ![表级别安全性](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  因为它可能会无意中访问引入到受保护的数据，行级安全性和对象级别安全性不能组合来自不同的角色。 在这种组合的角色的成员的用户的查询时生成错误。

*  如果它们引用的受保护的表或列，动态计算 （度量值，Kpi、 DetailRows） 会自动受到限制。 尽管没有任何机制来显式安全度量值，则可以通过更新要引用的受保护的表或列的表达式中隐式安全度量值。

*  受保护的列引用的关系处理假设不安全的列中的表。




## <a name="see-also"></a>另请参阅  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Roles 对象 (TMSL)](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
[表格模型脚本语言 (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
[表格对象模型 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)。

  
