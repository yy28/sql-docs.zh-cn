---
title: "STMPolyFromText (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STMPolyFromText (geometry Data Type)
- STMPolyFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromText (geometry Data Type)
ms.assetid: f087a61c-f063-4fb8-8f1c-251a2fed76a1
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8cc4ef5cbe61b6ccea9b898707814dd398838f5f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stmpolyfromtext-geometry-data-type"></a>STMPolyFromText（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**几何图形**实例传送开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式与任何 Z （仰角） 和 M （度量） 值的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STMPolyFromText ( 'multipolygon_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *multipolygon_tagged_text*  
 是的 WKT 表示形式**geometryMultiPolygon**您希望返回的实例。 *multipolygon_tagged_text*是**nvarchar (max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geometryMultiPolygon**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **Sql 几何图形**  
  
 OGC 类型： **MultiPolygon**  
  
## <a name="remarks"></a>注释  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STMPolyFromText()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPolyFromText('MULTIPOLYGON (((5 5, 10 5, 10 10, 5 5)), ((10 10, 100 10, 200 200, 30 30, 10 10)))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态几何图形方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  


