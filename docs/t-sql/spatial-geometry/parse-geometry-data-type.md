---
title: "分析 (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5800c6dba5cd962ba5aa218e90d33cf329e017c1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="parse-geometry-data-type"></a>Parse（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**几何图形**开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式的实例。 `Parse()`等效于[STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md)，出现异常，假定空间引用标识符 (SRID) 为 0 作为参数。 输入值可以根据需要包含 Z（标高）和 M（度量）值。
  
## <a name="syntax"></a>语法  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>参数  
 *geometry_tagged_text*  
 是的 WKT 表示形式**几何图形**您希望返回的实例。 *geometry_tagged_text*是**nvarchar**表达式。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 OGC 种**几何图形**返回实例`Parse()`设置为相应的 WKT 输入。  
  
 Null 将解释为 null 的字符串**几何图形**实例。  
  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Parse()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

