---
title: "STY (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STY_TSQL
- STY (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STY (geometry Data Type)
ms.assetid: f72e0eaa-7d1d-4052-88fd-a172d8cb0d71
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1f1478a2a92d756653c6c2435590a7a2bfeeed1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sty-geometry-data-type"></a>STY（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Y 坐标属性**点**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STY  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型： **float**  
  
 CLR 类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 此属性的值将为 null 如果**几何图形**实例是一个点。 该属性为只读。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `Point` 实例，并使用 `STY` 检索该实例的 Y 坐标。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STY;  
```  
  
## <a name="see-also"></a>另请参阅  
 [STX（geometry 数据类型）](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STSrid &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


