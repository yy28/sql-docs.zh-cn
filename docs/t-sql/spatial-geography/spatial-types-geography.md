---
title: "geography (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: geography
dev_langs: TSQL
helpviewer_keywords:
- geography data type [SQL Server], Transact-SQL
- spatial data types [SQL Server]
ms.assetid: d9e4952a-1841-4465-a64b-11e9288dba1d
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2f9a5b86f49e2d5e9b07908cd3c866999ff2f646
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="spatial-types---geography"></a>空间类型的地理位置
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Geography 空间数据类型， **geography**，作为.NET 公共语言运行时 (CLR) 数据类型中实现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此类型表示圆形地球坐标系中的数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 数据类型存储诸如 GPS 纬度和经度坐标之类的椭球体（圆形地球）数据。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的方法的一组**geography**空间数据类型。 这包括方法上**geography**由开放地理空间联盟 (OGC) 标准和一组定义[!INCLUDE[msCoName](../../includes/msconame-md.md)]该标准的扩展。  
 
 错误容差**geography**方法可以是 1.0 e 一样大-7 * 扩展盘区。 范围，该引用的点之间的近似的最大距离**geography**对象。
  

## <a name="registering-the-geography-type"></a>注册 geography 类型  
 **geography** 类型已进行预定义，可在每个数据库中使用。 你可以创建 **geography** 类型的表列并对 **geography** 数据进行操作，就像使用其他系统提供的数据类型一样。 可以用在持久化和非持久化计算列中。  
  
## <a name="examples"></a>示例  
  
### <a name="a-showing-how-to-add-and-query-geography-data"></a>A. 显示如何添加和查询地理数据  
 以下示例说明如何添加和查询地理数据。 第一个示例创建包含一个标识列和一个 `geography` 列 `GeogCol1` 的表。 第三列将 `geography` 列呈现为其开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式，并使用 `STAsText()` 方法。 接下来将插入两行：一行包含 `LineString` 类型的 `geography`实例，一行包含 `Polygon` 实例。  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653 , -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geography-instances"></a>B. 返回两个地域实例的交集  
 下面的示例使用 `STIntersection()` 方法返回以前插入的两个 `geography` 实例相交的点。  
  
```  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geography-in-a-computed-column"></a>C. 在计算列中使用地理数据  
 下面的示例创建一个表与持久化计算的列使用**geography**类型。  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geography,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)   

  
  
