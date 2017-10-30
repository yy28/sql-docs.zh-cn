---
title: "长时间 (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0c69ce921e8aa22d65011a56d47c5cd7b05ad76f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="long-geography-data-type"></a>Long（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  经度属性**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>返回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型： **float**  
  
 CLR 类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 在 OpenGIS 模型中，长时间定义仅在**geography**实例组成的单一点。 此属性将返回 NULL，如果**geography**实例包含多个单一点。 此属性是精确属性，且是只读的。  
  
## <a name="examples"></a>示例  
 此示例将创建**点**实例并检索点的经度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

