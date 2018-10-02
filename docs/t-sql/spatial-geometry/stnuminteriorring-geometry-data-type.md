---
title: STNumInteriorRing（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumInteriorRing_TSQL
- STNumInteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumInteriorRing (geometry Data Type)
ms.assetid: 48e78948-5b14-41dd-85d1-169bba1c4195
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0d2a1d1b8cea6a02b16b98edf57e3c92278599f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753834"
---
# <a name="stnuminteriorring-geometry-data-type"></a>STNumInteriorRing（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回 **Polygongeometry** 实例的内环数。
  
## <a name="syntax"></a>语法  
  
```  
  
.STNumInteriorRing ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：int  
  
 CLR 返回类型：SqlInt32  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 实例不是多边形，则此方法返回 null。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `Polygon` 实例并使用 `STNumInteriorRing()` 来确定该实例具有的内环数。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STNumInteriorRing();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

