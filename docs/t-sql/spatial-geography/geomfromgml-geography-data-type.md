---
title: "GeomFromGML (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geography Data Type)
- GeomFromGML method
ms.assetid: 470d0997-3cb0-4d34-9a45-b332fe432b14
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec0d21afb92b000f29fb91c4e3b848b4881b99c7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="geomfromgml-geography-data-type"></a>GeomFromGML（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

构造**geography**中给定的表示形式的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]地理标记语言 (GML) 的子集。
  
GML 的详细信息，请参阅以下的开放地理空间联盟规范： [OGC 规范，地域标记语言](http://go.microsoft.com/fwlink/?LinkId=93629)
  
这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。
  
## <a name="syntax"></a>语法  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>参数  
 *GML_input*  
 XML 输入，GML 将从该输入返回值。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geography**实例返回。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
 此方法将引发**ArgumentException**如果输入包含对跖边缘。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `GeomFromGml()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
 下面的示例使用 `GeomFromGml()` 创建 `FullGlobe``geography` 实例。  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<FullGlobe xmlns="http://schemas.microsoft.com/sqlserver/2011/geography" />';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态 Geography 方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

