---
title: STTouches（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STTouches (geometry Data Type)
- STTouches_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STTouches (geometry Data Type)
ms.assetid: af3650b4-26da-4600-9cc2-1be71dd76a14
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 18ea5efe0a0bc0ef4e84a5fa9d773a47f5eb99a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935649"
---
# <a name="sttouches-geometry-data-type"></a>STTouches（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果一个**geometry** 实例在空间上与另一个 **geometry** 实例接触，则返回 1。 否则，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STTouches ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 将与调用 `STTouches()` 的实例进行比较的另一个 geometry 实例  。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 如果两个 **geometry** 实例的点集相交，但是它们的内部不相交，则表明这两个实例接触。  
  
 如果 geometry 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null  。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STTouches()` 来测试两个 `geometry` 实例，以查看它们是否接触。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STTouches(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

