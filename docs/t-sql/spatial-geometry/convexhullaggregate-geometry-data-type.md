---
title: ConvexHullAggregate（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ConvexHullAggregate method (geometry)
ms.assetid: ca3d3b55-e02d-4599-8817-a54f5e047db8
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ff540360dc48dec0d13d6c0fe1093710263ac12f
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556007"
---
# <a name="convexhullaggregate-geometry-data-type"></a>ConvexHullAggregate（geometry 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

为一组给定的 **geometry** 对象返回一个凸包。
  
## <a name="syntax"></a>语法  
  
```  
  
ConvexHullAggregate ( geometry_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 *geometry_operand*  
 一个 **geometry** 类型的表列，表示一组 geometry 对象。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
## <a name="exception"></a>异常  
 在输入值无效时引发 `FormatException`。 请参阅 [STIsValid（geometry 数据类型）](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>备注  
 在输入为空或具有不同的 SRID 时，方法返回 null  。 请参阅[空间引用标识符 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 方法忽略 null 输入  。  
  
> [!NOTE]  
>  如果所有输入值均为 null，则方法返回 null   。  
  
## <a name="examples"></a>示例  
 下面的示例在一个表变量列中返回几何图形对象集的凸包。  
  
 ```
 -- Setup table variable for ConvexHullAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform ConvexHullAggregate on @Geom.shape column  
 SELECT geometry::ConvexHullAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

