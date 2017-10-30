---
title: "STAsText (geometry 数据类型) |Microsoft 文档"
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
- STAsText_TSQL
- STAsText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText (geometry Data Type)
ms.assetid: e0decf5e-2858-4c56-b61a-6123f47fb51c
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 127e64908ad9cb768d31e3c1ec42988962289246
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stastext-geometry-data-type"></a>STAsText（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回的开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式**几何图形**实例。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
  
## <a name="syntax"></a>语法  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **nvarchar (max)**  
  
 CLR 返回类型：**对**  
  
## <a name="examples"></a>示例  
 以下示例根据文本创建一个从 (0,0) 到 (2,3) 的 `LineString` geometry 实例。 `STAsText()` 以文本形式返回结果。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


