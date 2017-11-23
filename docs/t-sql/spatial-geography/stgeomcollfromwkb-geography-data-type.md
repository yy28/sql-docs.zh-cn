---
title: "STGeomCollFromWKB (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeomCollFromWKB (geography Data Type)
- STGeomCollFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMGeomCollFromWKB method
ms.assetid: bbed028c-9cd6-4236-b5e5-8e914a21f2e4
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4551839c69157e7ba1d5d24232661c9901f54aa6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomcollfromwkb-geography-data-type"></a>STGeomCollFromWKB（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**GeometryCollection**开放地理空间联盟 (OGC) 熟知二进制 (WKB) 表示形式的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *WKB_geometrycollection*  
 是的 WKB 表示形式**GeometryCollection**您希望返回的实例。 *WKB_geometrycollection*是**varbinary （max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**GeometryCollection**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**返回 STGeomCollFromWKB() 实例设置为**GeometryCollection**， **MultiPolygon**， **MultiLineString**，或**MultiPoint**，取决于相应的 WKB 输入。  
  
 此方法将引发**FormatException**如果输入不是格式正确的异常。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomCollFromWKB()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromWKB(0x01070000000200000001010000007593180456965EC017D9CEF753D34740010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
