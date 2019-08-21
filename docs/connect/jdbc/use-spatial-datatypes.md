---
title: 使用空间数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f133fa066ef2c486cf7bb40c5b653c99e077bc46
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026945"
---
# <a name="using-spatial-datatypes"></a>使用空间数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从 JDBC Driver preview release 6.5.0 开始支持空间数据类型 (几何和地理)。 存储过程、表值参数 (TVP)、BulkCopy 和 Always Encrypted 当前不支持空间数据类型。 此页显示使用 JDBC 驱动程序的 Geometry 和 Geography 数据类型的各种用例。 有关空间数据类型的概述, 请参阅[空间数据类型概述](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview)页。

## <a name="creating-a-geometry--geography-object"></a>创建几何/地理对象

可以通过两种主要方式来创建几何/地理对象-从熟知文本 (WKT) 或众所周知的二进制文件 (WKB) 进行转换。

### <a name="creating-from-wkt"></a>从 WKT 创建

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

这将创建一个具有空间引用系统标识符 (SRID) 0 的 LINESTRING Geometry 对象, 以及一个具有 SRID 4326 的 Geography 对象。

### <a name="creating-from-wkb"></a>从 WKB 创建

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

这将创建一个 Geometry 和 Geography 对象, 该对象等效于先前从 WKT 创建的对象。

## <a name="working-with-a-geometry--geography-object"></a>使用 Geometry/Geography 对象

假设用户在 SQL Server 上有一个表, 如下所示:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

用于插入几何值的示例脚本为:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

可以使用 Geography 列和**setGeography ()** 方法对地域对应项执行相同操作。

读取几何/地理列:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

可以使用 Geography 列和**getGeography ()** 方法对地域对应项执行相同操作。

## <a name="newly-introduced-apis"></a>新引入的 Api

这些是通过此添加引入的新公共 Api, 在类**SQLServerPreparedStatement**、 **SQLServerResultSet**、 **Geometry**和**Geography**中。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|描述|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 将指定参数设置为给定的 .sql 类对象。
|void setGeography(int n, Geography x)| 将指定参数设置为给定的 .sql 类对象。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|描述|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 返回此结果集对象的当前行中指定列的值作为 Java 编程语言中的 com. sqlserver 对象。
|Geometry getGeometry (字符串 columnName)| 返回此结果集对象的当前行中指定列的值作为 Java 编程语言中的 com. sqlserver 对象。
|Geography getGeography(int colunIndex)| 返回此结果集对象的当前行中指定列的值作为 Java 编程语言中的 com. sqlserver 对象。
|Geography getGeography (字符串 columnName)| 返回此结果集对象的当前行中指定列的值作为 Java 编程语言中的 com. sqlserver 对象。

### <a name="geometry"></a>Geometry

|方法|描述|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geometry 实例的构造函数，增加了该实例传递的任何 Z（标高）和 M（度量）值。
|Geometry STGeomFromWKB(byte[] wkb)| 开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式的 Geometry 实例的构造函数。
|反序列化几何 (byte [] wkb)| 用于从空间数据的内部 SQL Server 格式的 Geometry 实例的构造函数。
|Geometry 分析 (String wkt)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geometry 实例的构造函数。 空间引用标识符默认为0。
|几何图形点 (double x, double y, int SRID)| Geometry 实例的构造函数, 该构造函数表示点实例的 X 和 Y 值以及空间引用标识符。
|String STAsText ()| 返回 Geometry 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
|byte[] STAsBinary()| 返回 Geometry 实例的开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式。 此值不包含该实例传递的任何 Z 或 M 值。
|byte[] serialize()| 返回表示 Geometry 类型的内部 SQL Server 格式的字节。
|布尔 hasM ()| 如果对象包含 M (度量) 值, 则返回。
|布尔 hasZ ()| 如果对象包含 Z (仰角) 值, 则返回。
|Double getX()| 返回 X 坐标值。
|Double getY()| 返回 Y 坐标值。
|Double getM()| 返回对象的 M (度量) 值。
|Double getZ()| 返回对象的 Z (仰角) 值。
|int getSrid()| 返回空间引用标识符 (SRID) 值。
|boolean isNull()| 如果 Geometry 对象为 null, 则返回。
|int STNumPoints ()| 返回 Geometry 对象中的点数。
|String STGeometryType()| 返回由几何图形实例表示的开放地理空间联盟 (OGC) 类型名称。
|String asTextZM()| 返回 Geometry 对象的已知文本 (WKT) 表示形式。
|String toString ()| 返回 Geometry 对象的字符串表示形式。

### <a name="geography"></a>Geography

|方法|描述|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geography 实例的构造函数，增加了该实例传递的任何 Z（标高）和 M（度量）值。
|Geography STGeomFromWKB(byte[] wkb)| 开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式的 Geography 实例的构造函数。
|地域反序列化 (byte [] wkb)| 地理实例的构造函数, 来自空间数据的内部 SQL Server 格式。
|地域解析 (String wkt)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geography 实例的构造函数。 空间引用标识符默认为0。
|地理点 (双 lon, double lat, int SRID)| 地理实例的构造函数，它表示来自其经纬度的点实例和空间引用标识符。
|String STAsText ()| 返回 Geography 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
|byte[] STAsBinary())| 返回 Geography 实例的开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式。 此值不包含该实例传递的任何 Z 或 M 值。
|byte[] serialize()| 返回表示 Geography 类型的内部 SQL Server 格式的字节。
|布尔 hasM ()| 如果对象包含 M (度量) 值, 则返回。
|布尔 hasZ ()| 如果对象包含 Z (仰角) 值, 则返回。
|Double getLatitude()| 返回纬度值。
|Double getLongitude()| 返回经度值。
|Double getM()| 返回对象的 M (度量) 值。
|Double getZ()| 返回对象的 Z (仰角) 值。
|int getSrid()| 返回空间引用标识符 (SRID) 值。
|boolean isNull()| 如果 Geography 对象为 null, 则返回。
|int STNumPoints ()| 返回 Geography 对象中的点数。
|String STGeographyType()| 返回由地域实例表示的开放地理空间联盟 (OGC) 类型名称。
|String asTextZM()| 返回 Geography 对象的已知文本 (WKT) 表示形式。
|String toString ()| 返回 Geography 对象的字符串表示形式。

## <a name="limitations-of-spatial-datatypes"></a>空间数据类型的限制

1. 仅支持从 SQL Server 2012 及更高版本开始支持空间子数据类型**CircularString**、 **CompoundCurve**、 **CurvePolygon**和**FullGlobe** 。

2. Always Encrypted 不能与空间数据类型一起使用。

3. 空间数据类型当前不支持存储过程、TVP 和 BulkCopy 操作。

## <a name="see-also"></a>另请参阅

[空间数据类型示例 (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
