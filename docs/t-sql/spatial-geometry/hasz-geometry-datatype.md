---
title: "HasZ (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: HasZ geometry
ms.assetid: aa378943-252a-4079-848b-6c59344fcfce
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 941387fd3c293a60069e42294d6213928fb00418
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="hasz-geometry-datatype"></a>HasZ（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果空间对象包含至少一个 Z 值，则返回 1 (true)；否则返回 0 (false)。  
  
## <a name="syntax"></a>语法  
  
```  
  
.HasZ  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型：**布尔**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>示例  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  
