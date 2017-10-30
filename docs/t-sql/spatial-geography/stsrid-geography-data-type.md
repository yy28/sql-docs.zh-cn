---
title: "STSrid (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c93ccfc28eb3dfe3b24a817394bf3481a86e89d3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stsrid-geography-data-type"></a>STSrid（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid**是一个整数，表示实例的空间引用标识符 (SRID)。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STSrid  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型： **int**  
  
 CLR 类型： **SqlInt32**  
  
## <a name="remarks"></a>注释  
 此属性可以进行修改。  
  
## <a name="examples"></a>示例  
 第一个示例创建 SRID 值为 4326 (WGS84) 的 `geography` 实例并使用 `STSrid` 来确认该 SRID。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 第二个示例使用 `STSrid` 将实例的 SRID 值更改为 4267 (NAD27)，然后确认修改后的 SRID 值。  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [空间引用标识符 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  

