---
title: "HasZ (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 05/04/2017
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
- HasZ
- HasZ_TSQL
dev_langs: TSQL
helpviewer_keywords: HasZ geography
ms.assetid: 4c5e1669-a987-4dda-9ebf-f573ce615c34
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7725a6a28d6c1ea22da12519819933f898c44684
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="hasz-geography-data-type"></a>HasZ（geography 数据类型）
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
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
