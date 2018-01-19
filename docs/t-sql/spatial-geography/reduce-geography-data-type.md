---
title: "减少 (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs: TSQL
helpviewer_keywords: Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1932373b11b10724bbbb4e05863428012eb23eb
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="reduce-geography-data-type-"></a>Reduce（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回可大概了解给定**geography**实例生成的具有给定容差的实例上运行道格拉斯 • Peucker 算法。  
  
 这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>参数  
  
|||  
|-|-|  
|术语|定义|  
|*tolerance*|是类型的值**float**。 *容差*是要输入到道格拉斯 • Peucker 算法的容差。 *容差*必须为正数。|  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 有关集合类型，此算法对独立每**geography**实例中包含。 此算法不会修改**点**实例。  
  
 此方法将尝试保留的终结点**LineString**实例，但可能会失败，若要这样做以保持有效的结果。  
  
 如果`Reduce()`调用此方法将生成一个含有负值， **ArgumentException**。 在 `Reduce()` 中使用的公差必须为正数。  
  
 · 道格拉斯 Peucker 算法在每个的工作原理曲线或环位于**geography**通过删除起点和终点除外的所有点的实例。 删除每个点随后将被添加回来，直到没有点开头最远的美属外点，多个*容差*结果中。 然后，如果必要，使结果变得有效，因为必须保证有一个有效的结果。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，此方法已扩展到**FullGlobe**实例。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
 以下示例创建一个 `LineString` 实例，并使用 `Reduce()` 简化该实例。  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
