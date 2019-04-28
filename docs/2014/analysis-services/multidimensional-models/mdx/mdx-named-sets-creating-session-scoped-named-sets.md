---
title: 创建会话作用域的命名集 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- CREATE SET statement
- session-scoped named sets [MDX]
ms.assetid: b751e1e4-6d4c-4d36-a28d-ffdaaee0f1c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96b34d8b3fd2dce31f604c50a7431b993a29beca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699582"
---
# <a name="creating-session-scoped-named-sets-mdx"></a>创建会话作用域的命名集 (MDX)
  若要创建在整个多维表达式 (MDX) 会话期间都可用的命名集，请使用 [CREATE SET](/sql/mdx/mdx-data-definition-create-set) 语句。 直到 MDX 会话关闭后才会删除使用 CREATE SET 语句创建的命名集。  
  
 如本主题中所介绍，WITH 关键字的语法很直观且易于使用。  
  
> [!NOTE]  
>  有关命名集的详细信息，请参阅[在 MDX 中生成命名集 (MDX)](mdx-named-sets-building-named-sets.md)。  
  
## <a name="create-set-syntax"></a>CREATE SET 语法  
 CREATE SET 语句的语法如下：  
  
```  
CREATE SESSION SET [CURRENTCUBE. | <cube name>.]<Set Identifier> AS <Set Expression>  
```  
  
 在 CREATE SET 语法中， `cube name` 参数包含多维数据集的名称，该多维数据集包含命名集的成员。 如果未指定 `cube name` 参数，则当前的多维数据集将用作包含命名集的成员的多维数据集。 另外， `Set_Identifier` 参数包含命名集的别名， `Set_Expression` 参数包含命名集别名引用的集表达式。  
  
## <a name="create-set-example"></a>CREATE SET 示例  
 下面的示例使用 CREATE SET 语句创建基于 Store 多维数据集的 `SetCities_2_3` 命名集。 `SetCities_2_3` 命名集的成员是位于 City 2 和 City 3 的商店。  
  
```  
create Session set [Store].[SetCities_2_3] as  
{[Data Stores].[ByLocation].[State].&[CA].&[City 02],  
[Data Stores].[ByLocation].[State].&[NH].&[City 03]}  
```  
  
 通过使用 CREATE SET 语句定义 `SetCities_2_3` 命名集，此命名集在当前 MDX 会话期间将始终可用。 下面的示例是一个将返回 City 2 和 City 3 成员的有效查询，该查询可在创建 `SetCities_2_3` 命名集后、结束会话前的任何时间运行。  
  
```  
select SetCities_2_3 on 0 from [Store]  
```  
  
## <a name="see-also"></a>请参阅  
 [创建查询作用域的命名集 (MDX)](mdx-named-sets-creating-query-scoped-named-sets.md)  
  
  
