---
title: "插入、 更新和删除成员 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d98ad262e92a1da61c6ac3dda67aaac871dabd1e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>插入、更新和删除成员 (XMLA)
  你可以使用[插入](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，和[删除](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)XML 中的命令为 Analysis (XMLA) 来分别插入、 更新或从允许写维度中删除成员。 关于启用写功能的维度的详细信息，请参阅[Write-Enabled 维度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="inserting-new-members"></a>插入新成员  
 **插入**命令将新成员插入到写入的维度中的指定属性。  
  
 之前构造**插入**命令时，你应具有可用于要插入的新成员的以下信息：  
  
-   要在其中插入新成员的维度。  
  
-   要在其中插入新成员的维度特性。  
  
-   新成员的名称，包括该名称的所有适用翻译。  
  
-   新成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
-   不作为该维度内的其他特性实现的所有适用特性属性的值。 此类特性属性包括一元运算符、翻译、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
 **插入**命令采用只有两个属性：  
  
-   [对象](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)属性，其中包含在其中的成员是要插入的维度对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   [属性](../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)属性，其中包含一个或多个[属性](../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)元素来标识成员要插入的属性。 每个**属性**元素标识属性并提供名称、 值、 翻译、 一元运算符、 自定义汇总、 自定义汇总属性，并跳过单个成员添加到的标识属性的级别。  
  
    > [!NOTE]  
    >  所有属性**属性**元素必须包含。 否则，可能会出错。  
  
## <a name="updating-existing-members"></a>更新现有成员  
 **更新**命令更新指定的特性，根据它们与其他写入的维度中的属性中的其他成员关系中的现有成员。 **更新**命令可以移动成员复制到层次结构中的其他层所包含的维度，并可用于重构由父属性定义的父-子层次结构。  
  
 之前构造**更新**命令时，你应具有可用于要更新的成员的以下信息：  
  
-   要在其中更新现有成员的维度。  
  
-   要在其中更新现有成员的维度特性。  
  
-   现有成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
-   不作为该维度内的其他特性实现的所有适用特性属性的值。 此类特性属性包括一元运算符、翻译、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
 **更新**命令采用仅三个必需的属性：  
  
-   **对象**属性，其中包含在其中的成员是要更新的维度对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   **属性**属性，其中包含一个或多个**属性**元素来标识成员要更新的属性。 **属性**元素标识属性并提供了名称、 值、 翻译、 一元运算符、 自定义汇总和自定义汇总属性，并跳过单个成员经过更新以标识属性级别。  
  
    > [!NOTE]  
    >  所有属性**属性**元素必须包含。 否则，可能会出错。  
  
-   [其中](../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)属性，其中包含一个或多个**属性**约束成员要更新的属性的元素。 **其中**属性至关重要限制**更新**命令的成员的特定实例。 如果**其中**属性未指定，则更新的给定成员的所有实例。 例如，有三个客户，您希望将他们的市县名称从 Redmond 更改为 Bellevue。 若要更改的城市名称，必须提供**其中**属性，用于标识客户中的三个成员属性，则为更改 City 属性中的成员。 如果不提供此**其中**属性，每个客户的城市名称当前为 Redmond 将具有贝尔维尤后的城市名称**更新**命令将运行。  
  
    > [!NOTE]  
    >  新成员，除了**更新**命令仅可更新属性中未包括的属性的密钥值**其中**子句。 例如，更新客户时不能更新市县名称；否则，会更改所有客户的市县名称。  
  
### <a name="updating-members-in-parent-attributes"></a>更新父特性中的成员  
 若要支持父属性**更新**命令可选[MoveWithDescendants](../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md)MovewithDescedants 属性。 设置**MoveWithDescendants**属性为 true 指示当该父成员的标识符更改后，还应的后代中的父成员与父成员中移动。 如果将此值设置为 False，则移动某父成员将导致该父成员的直接后代提升到该父成员先前所处的级别。  
  
 更新一个父属性中的成员时**更新**命令无法更新其他属性中的成员。  
  
## <a name="dropping-existing-members"></a>删除现有成员  
 之前构造**删除**命令时，你应具有可用于要删除的成员的以下信息：  
  
-   要在其中删除现有成员的维度。  
  
-   要在其中删除现有成员的维度特性。  
  
-   要删除的现有成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
 **删除**命令采用只有两个必需的属性：  
  
-   **对象**属性，其中包含在其中的成员是要删除的维度对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   **其中**属性，其中包含一个或多个**属性**约束是用要删除成员属性的元素。 **其中**属性至关重要限制**删除**命令的成员的特定实例。 如果**其中**命令未指定，则将删除给定成员的所有实例。 例如，您希望从 Redmond 中删除三个客户。 若要删除这些客户，你必须提供**其中**属性，它标识要删除客户属性中的三个成员和 City 属性是要删除的三个客户的 Redmond 成员。 如果**其中**属性仅指定城市属性的 Redmond 成员，将被丢弃 Redmond 与关联的每个客户**删除**命令。 如果**其中**属性仅在客户属性指定的三个成员，将通过完全删除的三个客户**删除**命令。  
  
    > [!NOTE]  
    >  **属性**中包含的元素**删除**命令必须仅包含**AttributeName**和**密钥**属性。 否则，可能会出错。  
  
### <a name="dropping-members-in-parent-attributes"></a>删除父特性中的成员  
 设置[DeleteWithDescendants](../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md)属性指示父成员的后代还应删除与父成员。 如果将此值设置为 False，则父成员的直接后代将提升到该父成员先前所处的级别。  
  
> [!IMPORTANT]  
>  用户只需删除父成员的权限，即可删除父成员及其后代。 用户无需删除后代的权限。  
  
## <a name="see-also"></a>另请参阅  
 [删除元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [更新元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [定义和标识对象 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
