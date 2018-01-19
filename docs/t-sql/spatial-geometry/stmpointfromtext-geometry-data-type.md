---
title: "STMPointFromText (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
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
- STMPointFromText (geometry Data Type)
- STMPointFromText_TSQL
dev_langs: TSQL
helpviewer_keywords: STMPointFromText (geometry Data Type)
ms.assetid: 37059074-5ee8-4f55-9414-1e958fd3adaf
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f639e9027c6844c9c65c9eb667e64b5446096d46
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="stmpointfromtext-geometry-data-type"></a>STMPointFromText（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**几何图形**实例传送开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式扩充任何 Z （仰角） 和 M （度量） 值的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STMPointFromText ( 'multipoint_tagged_text', SRID )  
```  
  
## <a name="arguments"></a>参数  
 *multipoint_tagged_text*  
 是的 WKT 表示形式**geometryMultiPoint**您希望返回的实例。 *multipoint_tagged_text*是**nvarchar (max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geometryMultiPoint**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 OGC 类型： **MultiPoint**  
  
## <a name="remarks"></a>注释  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STMPointFromText()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromText('MULTIPOINT ((100 100), (200 200))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态几何图形方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

