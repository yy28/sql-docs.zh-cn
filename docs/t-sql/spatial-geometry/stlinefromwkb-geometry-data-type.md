---
title: "STLineFromWKB (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STLineFromWKB (geometry Data Type)
- STLineFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STLineFromWKB (geometry Data Type)
ms.assetid: e674c8c4-c67f-4fc1-9873-d9c2ed46c659
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 94ef2360ce423adb2edf085a160ee3b516c605e2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stlinefromwkb-geometry-data-type"></a>STLineFromWKB（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

返回**geometryLineString**开放地理空间联盟 (OGC) 熟知二进制 (WKB) 表示形式的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *WKB_linestring*  
 是的 WKB 表示形式**geometryLineString**您希望返回的实例。 *WKB_linestring*是**varbinary （max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geometryLineString**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 OGC 类型： **LineString**  
  
## <a name="remarks"></a>注释  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STLineFromWKB()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STLineFromWKB(0x0102000000020000000000000000005940000000000000594000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态几何图形方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

