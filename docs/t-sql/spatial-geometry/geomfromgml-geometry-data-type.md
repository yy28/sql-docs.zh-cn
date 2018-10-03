---
title: GeomFromGml（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geometry Data Type)
ms.assetid: a3f2c84b-a49f-4ce3-ba25-b903fb0c99b4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4d99624d21eb59862c556bc1a4f559ed8a9d9b20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835715"
---
# <a name="geomfromgml-geometry-data-type"></a>GeomFromGml（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

根据地理标记语言 (GML) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 子集中的给定表示形式构建 geometry 实例。
  
有关地理标记语言的详细信息，请参阅以下开放地理空间信息联盟规范：
  
[OGC 规范：地理标记语言](http://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>语法  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>参数  
 GML_input  
 XML 输入，GML 将从该输入返回值。  
  
 SRID  
 一个 int 表达式，表示希望返回的 geometry 实例的空间引用 ID (SRID)。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 如果输入的格式不正确，此方法将引发 FormatException。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `GeomFromGml()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"> <posList>100 100 20 180 180 180</posList> </LineString>';  
SET @g = geometry::GeomFromGml(@x, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

