---
title: CollectionAggregate（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba8de4fd1dbdf4d7eee55b12c60da7156f512679
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36245719"
---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

从一组 geometry 类型创建一个 GeometryCollection 实例。
  
## <a name="syntax"></a>语法  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>参数  
 *geometry_operand*  
 geometry 类型表列，表示要在 GeometryCollection 实例中列出的一组 geometry 对象。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
## <a name="exceptions"></a>异常  
 在输入值无效时引发 `FormatException`。 请参阅 [STIsValid（geometry 数据类型）](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 在输入为空或具有不同的 SRID 时，方法返回 null。 请参阅[空间引用标识符 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 方法忽略 null 输入。  
  
> [!NOTE]  
>  如果所有输入值均为 null，则方法返回 null。  
  
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
  
  

