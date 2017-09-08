---
title: "STLineFromText (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STLineFromText (geography Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText method
ms.assetid: e0c05bde-077d-4ce2-b4ec-8861db9b996d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7137023a0c382a5114abae4676a5aead8c700f0d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stlinefromtext-geography-data-type"></a>STLineFromText（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**geography**实例传送开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式，扩充任何 Z （仰角） 和 M （度量） 值的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *linestring_tagged_text*  
 是的 WKT 表示形式**geographyLineString**您希望返回的实例。 *linestring_tagged_text*是**nvarchar (max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geographyLineString**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
 OGC 类型： **LineString**  
  
## <a name="remarks"></a>注释  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STLineFromText()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地域方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

