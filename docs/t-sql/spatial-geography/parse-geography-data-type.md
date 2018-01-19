---
title: "分析 (geography 数据类型) |Microsoft 文档"
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
dev_langs: TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32d8925fdf53a1d0bcac33719348138b354376c2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="parse-geography-data-type"></a>Parse（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**geography**开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式的实例。 Parse （） 等效于[STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)，只不过它假定空间引用标识符 (SRID) 的 4326 作为参数。 输入值可以根据需要包含 Z（标高）和 M（度量）值。
  
这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。
  
## <a name="syntax"></a>语法  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>参数  
 *geography_tagged_text*  
 是的 WKT 表示形式**geography**实例返回。 *geography_tagged_text*是**nvarchar**表达式。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**返回实例`Parse()`设置为相应的 WKT 输入。  
  
 Null 将解释为 null 的字符串**geography**实例。  
  
 此方法将引发**ArgumentException**如果输入包含对跖边缘。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Parse()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态 Geography 方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText（geography 数据类型）](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
