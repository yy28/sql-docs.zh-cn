---
title: "STSrid (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STSrid (geometry Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid (geometry Data Type)
ms.assetid: 5e0de983-a0fe-48b7-9e08-30588d7271e2
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e8e29a1a5446713c94462bdcf4d0c252875d7c0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stsrid-geometry-data-type"></a>STSrid（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid**是一个整数，表示实例的空间引用标识符。  
  
此属性可以进行修改。
  
## <a name="syntax"></a>语法  
  
```  
  
STSrid  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型： **int**  
  
 CLR 类型： **SqlInt32**  
  
## <a name="examples"></a>示例  
 第一个示例创建**几何图形**13 并使用实例的 SRID 值`STSrid`以确认 SRID。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 13);  
SELECT @g.STSrid;  
```  
  
 第二个示例使用 `STSrid` 将该实例的 SRID 值更改为 23，然后确认修改后的 SRID 值。  
  
```  
SET @g.STSrid = 23;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>另请参阅  
 [STX（geometry 数据类型）](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY（geometry 数据类型）](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


