---
title: STGeomCollFromWKB（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomCollFromWKB (geometry Data Type)
- STGeomCollFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomCollFromWKB (geometry Data Type)
ms.assetid: 6c55032c-7f5e-4181-8e67-c0265032db63
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 337e2bf7f75dc80f3abc077bd7c43f9e80a4758d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762491"
---
# <a name="stgeomcollfromwkb-geometry-data-type"></a>STGeomCollFromWKB（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

从开放地理空间信息联盟 (OGC) 已知二进制 (WKB) 表示形式中返回 **geometrycollection** 实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 WKB_geometrycollection   
 希望返回的 **geometrycollection** 实例的 WKB 表示形式。 WKB_geometrycollection 是一个 varbinary(max) 表达式   。  
  
 SRID   
 一个 int 表达式，表示希望返回的 geometry 实例的空间引用 ID (SRID)   。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
 CLR 返回类型：SqlGeometry   
  
## <a name="remarks"></a>备注  
 `STGeomCollFromWKB()` 返回的 geometry 实例的 OGC 类型设置为 GeomCollection、MultiPolygon、MultiLineString 或 MultiPoint，具体取决于相应的 WKB 输入。  
  
 如果输入格式不正确，此方法会抛出 FormatException 异常。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomCollFromWKB()` 创建 geometry 实例  。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromWKB(0x0107000000020000000103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440010100000000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态几何图形方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
