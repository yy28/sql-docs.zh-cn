---
title: STInteriorRingN （geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STInteriorRingN_TSQL
- STInteriorRingN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STInteriorRingN (geometry Data Type)
ms.assetid: 47310f9f-2cdb-41e0-a6da-7c3cfbf139ac
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a1de9fabd5c7f3dcfd7fd128599bc03b7489d033
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stinteriorringn-geometry-data-type"></a>STInteriorRingN（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回 Polygongeometry 实例的指定内环。
  
## <a name="syntax"></a>语法  
  
```  
  
.STInteriorRingN ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 一个 int 表达式，其值介于 1 和 geometry 实例中的内环数之间。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
 开放地理空间信息联盟 (OGC) 类型：LineString  
  
## <a name="remarks"></a>Remarks  
 如果 geometry 实例不是多边形，则此方法返回 NULL。 如果表达式大于环数，则此方法还将引发 ArgumentOutOfRangeException。 可以使用 `STNumInteriorRing``()` 返回环数。  
  
## <a name="examples"></a>示例  
 以下示例创建 `Polygon` 实例，并使用 `STInteriorRingN()` 以LineString 的形式返回多边形的内环 。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STInteriorRingN(1).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

