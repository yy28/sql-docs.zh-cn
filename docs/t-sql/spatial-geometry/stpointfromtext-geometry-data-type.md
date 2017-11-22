---
title: "STPointFromText (geometry 数据类型) |Microsoft 文档"
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
- STPointFromText_TSQL
- STPointFromText (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STPointFromText (geometry Data Type)
ms.assetid: 1d71dfd8-9d80-44c3-b6e1-64e99cde1fa0
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a63ebffa22079c146593229e3525e5173c0531ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stpointfromtext-geometry-data-type"></a>STPointFromText（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**几何图形**实例传送开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式扩充任何 Z （仰角） 和 M （度量） 值的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STPointFromText ( 'point_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *point_tagged_text*  
 是的 WKT 表示形式**geometryPoint**您希望返回的实例。 *point_tagged_text*是**nvarchar (max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geometryPoint**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 OGC 类型：**点**  
  
## <a name="remarks"></a>注释  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STPointFromText()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STPointFromText('POINT (100 100)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态几何图形方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

