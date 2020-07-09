---
title: STMPolyFromWKB（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPolyFromWKB (geometry Data Type)
- STMPolyFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromWKB (geometry Data Type)
ms.assetid: cac25868-08ef-46fc-9c3d-a15e43794a7a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8957857f11f993a09cae4604a89178ef66856b86
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762299"
---
# <a name="stmpolyfromwkb-geometry-data-type"></a>STMPolyFromWKB（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

从开放地理空间信息联盟 (OGC) 已知二进制 (WKB) 表示形式返回 **geometryMultiPolygon** 实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STMPolyFromWKB ( 'WKB_multipolygon' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 WKB_multipolygon   
 希望返回的 **geometryMultiPolygon** 实例的 WKB 表示形式。 WKB_multipolygon 是一个 varbinary(max) 表达式   。  
  
 SRID   
 一个 int 表达式，表示希望返回的 geometryMultiPolygon 实例的空间引用 ID (SRID)   。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
 CLR 返回类型：SqlGeometry   
  
 OGC 类型：MultiPolygon   
  
## <a name="remarks"></a>备注  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STMPolyFromWKB()` 创建 `geometry` 实例：  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPolyFromWKB(0x0106000000020000000103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440010300000001000000050000000000000000002440000000000000244000000000000059400000000000002440000000000000694000000000000069400000000000003E400000000000003E4000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态几何图形方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

