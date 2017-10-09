---
title: "CollectionAggregate (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2acf5b0fe7f3b6833f56f5264844e4dc9870155f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

创建**GeometryCollection**从一组实例**几何图形**类型。
  
## <a name="syntax"></a>语法  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>参数  
 *geometry_operand*  
 是**几何图形**类型表示的一组表列**几何图形**对象被列入**GeometryCollection**实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
## <a name="exceptions"></a>异常  
 在输入值无效时引发 `FormatException`。 请参阅[STIsValid &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>注释  
 方法返回**null**时输入为空或输入具有不同 Srid。 请参阅[空间引用标识符 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 方法将忽略**null**输入。  
  
> [!NOTE]  
>  方法返回**null**如果所有输入的值为**null**。  
  
## <a name="examples"></a>示例  
 以下示例返回一个包含 `GeometryCollection` 和 `CurvePolygon` 的 `Polygon` 实例。  
  
 ```
 -- Setup table variable for CollectionAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform CollectionAggregate on @Geom.shape column  
 SELECT geometry::CollectionAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


