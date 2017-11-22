---
title: "STGeomCollFromText (geography 数据类型) |Microsoft 文档"
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
- STGeomCollFromText_TSQL
- STGeomCollFromText (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STGeomCollFromText method
ms.assetid: a5b3c344-1045-43a4-82fa-47f6206a288e
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c096421e5d318d38ecc4afb7ef10b62f970cf1a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomcollfromtext-geography-data-type"></a>STGeomCollFromText（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**geography**实例传送开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式，扩充任何 Z （仰角） 和 M （度量） 值的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *geometrycollection_tagged_text*  
 是的 WKT 表示形式**geography**您希望返回的实例。 *geometrycollection_tagged_text*是**nvarchar (max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geography**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**返回 STGeomCollFromText() 实例设置为相应的 WKT 输入。  
  
 此方法将引发**ArgumentException**如果输入无效。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomCollFromText()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromText('GEOMETRYCOLLECTION ( POINT(-122.34900 47.65100), LINESTRING(-122.360 47.656, -122.343 47.656) )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
