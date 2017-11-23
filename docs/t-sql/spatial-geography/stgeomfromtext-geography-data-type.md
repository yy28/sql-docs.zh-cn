---
title: "STGeomFromText (geography 数据类型) |Microsoft 文档"
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
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e781cdd50bd10711d181318cb584f6949828e19d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**geography**实例传送开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式扩充任何 Z （仰角） 和 M （度量） 值的实例。
  
这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *geography_tagged_text*  
 是的 WKT 表示形式**geography**实例返回。 *geography_tagged_text*是**nvarchar (max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geography**实例返回。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**返回 STGeomFromText() 实例设置为相应的 WKT 输入。  
  
 此方法将引发**ArgumentException**如果输入包含对跖边缘。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomFromText()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
