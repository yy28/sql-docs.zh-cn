---
title: "AsGml (geometry 数据类型) |Microsoft 文档"
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
- AsGml(geometry_Data_Type)_TSQL
- AsGml
- AsGml(geometry Data Type)
- AsGml_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml (geometry Data Type)
ms.assetid: f6c2e130-05f3-4ef3-921b-d78b51437d48
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a4ca0fcd5b8b7b4ffdb39d3201f7060efe18a74
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="asgml-geometry-data-type"></a>AsGml（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回的地理标记语言 (GML) 表示形式**几何图形**实例。
  
有关地域标记语言的详细信息，请参阅以下的开放地理空间联盟规范：[OGC 规范，地域标记语言。](http://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>语法  
  
```  
  
.AsGml ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **xml**  
  
 CLR 返回类型： **SqlXml**  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例，并使用 `AsGML()` 返回实例的 GML 说明。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0)  
SELECT @g.AsGml();  
```  
  
 此方法将描述返回为 `LineString` 实例。  
  
```  
<LineString xmlns="http://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


