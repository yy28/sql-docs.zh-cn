---
title: "STEnvelope (geometry 数据类型) |Microsoft 文档"
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
- STEnvelope_TSQL
- STEnvelope (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STEnvelope (geometry Data Type)
ms.assetid: 781d22e9-38df-4c23-836f-6dd0bdef49c5
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b01e09313f96872ac8e4284d73077a560b2d3dbc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stenvelope-geometry-data-type"></a>STEnvelope（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回实例的最小轴对齐边界矩形。
  
## <a name="syntax"></a>语法  
  
```  
  
STEnvelope ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomFromText()` 创建从 (0,0) 到 (2,3) 的 `LineString` 实例，并使用 `STEnvelope()` 返回 `LineString` 的边界框。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STEnvelope().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


