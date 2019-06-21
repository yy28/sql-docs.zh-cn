---
title: 使用空间数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ce3df0755799e907bb286e10f5711a58a48135bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782464"
---
# <a name="using-spatial-datatypes"></a>正在使用空间数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从 JDBC 驱动程序预览版本 6.5.0 支持空间数据类型 （Geometry 和 Geography）。 使用存储的过程、 表值参数 (TVP)、 BulkCopy，和 Always Encrypted 目前不支持空间数据类型。 此页显示各种用例的 Geometry 和 Geography 数据类型和 JDBC 驱动程序。 有关空间数据类型的概述，请[空间数据类型概述](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview)页。

## <a name="creating-a-geometry--geography-object"></a>创建几何图形 / 地理对象

有两种主要方法来创建几何图形 / 地理对象-是转换从熟知文本 (WKT) 或熟知二进制 (WKB)。

### <a name="creating-from-wkt"></a>创建从 WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

这将使用 SRID 4326 创建 LINESTRING 几何图形对象的空间引用系统标识符 (SRID) 0 和地理对象。

### <a name="creating-from-wkb"></a>创建从 WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

这将创建一个 Geometry 和 Geography 对象，它等效于从 WKT 以前创建的。

## <a name="working-with-a-geometry--geography-object"></a>使用几何 / 地理对象

假定用户有一个表，如下面的 SQL Server 上：

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

将插入的几何值的示例脚本：

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

可以使用地理位置列的地理位置对应的实现相同和**setGeography()** 方法。

若要读取几何图形 / 地理位置列：

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

可以使用地理位置列的地理位置对应的实现相同和**getGeography()** 方法。

## <a name="newly-introduced-apis"></a>新引入的 Api

这些是已添加此元素后，在类中引入的新公共 Api **SQLServerPreparedStatement**， **SQLServerResultSet**， **Geometry**，并且**Geography**。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|描述|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 将指定的参数设置为给定的 microsoft.sql.Geometry 类对象。
|void setGeography(int n, Geography x)| 将指定的参数设置为给定的 microsoft.sql.Geography 类对象。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|描述|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 此结果集对象的当前行中将返回指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geometry 对象。
|Geometry getGeometry (字符串 columnName)| 此结果集对象的当前行中将返回指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geometry 对象。
|Geography getGeography(int colunIndex)| 此结果集对象的当前行中将返回指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geography 对象。
|Geography getGeography (字符串 columnName)| 此结果集对象的当前行中将返回指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geography 对象。

### <a name="geometry"></a>Geometry

|方法|描述|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geometry 实例的构造函数，增加了该实例传递的任何 Z（标高）和 M（度量）值。
|Geometry STGeomFromWKB(byte[] wkb)| 开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式的 Geometry 实例的构造函数。
|几何图形反序列化 (byte [] wkb)| 从空间数据的内部 SQL Server 格式的 Geometry 实例的构造函数。
|Geometry 分析 (字符串 wkt)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geometry 实例的构造函数。 空间引用标识符是默认设置为 0。
|几何点 （双精度型 x，y double，int SRID）| 根据其 X 和 Y 值以及空间引用标识符表示的点实例的几何图形实例的构造函数。
|字符串 stastext （)| 返回 Geometry 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
|byte[] STAsBinary()| 返回 Geometry 实例的开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式。 此值不包含该实例传递的任何 Z 或 M 值。
|byte[] serialize()| 返回表示 Geometry 类型的内部 SQL Server 格式的字节。
|布尔 hasM()| 返回对象是否包含 M （度量） 值。
|布尔 hasZ()| 返回对象是否包含 Z （标高） 值。
|Double getX()| 返回 X 坐标值。
|Double getY()| 返回 Y 坐标值。
|Double getM()| 返回的对象的 M （度量） 值。
|Double getZ()| 返回的对象的 Z （标高） 值。
|int getSrid()| 返回的空间引用标识符 (SRID) 值。
|boolean isNull()| 返回的 Geometry 对象是否为 null。
|int STNumPoints()| 返回的 Geometry 对象中的点数。
|String STGeometryType()| 返回由几何图形实例表示的开放地理空间联盟 (OGC) 类型名称。
|String asTextZM()| 返回几何图形对象的熟知文本 (WKT) 表示形式。
|字符串 tostring （)| 返回几何图形对象的字符串表示形式。

### <a name="geography"></a>Geography

|方法|描述|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geography 实例的构造函数，增加了该实例传递的任何 Z（标高）和 M（度量）值。
|Geography STGeomFromWKB(byte[] wkb)| 开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式的 Geography 实例的构造函数。
|Geography 反序列化 (byte [] wkb)| 从空间数据的内部 SQL Server 格式的 Geography 实例的构造函数。
|Geography 分析 (字符串 wkt)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geography 实例的构造函数。 空间引用标识符是默认设置为 0。
|地理点 （双 lon，lat double，int SRID）| 地理实例的构造函数，它表示来自其经纬度的点实例和空间引用标识符。
|字符串 stastext （)| 返回 Geography 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
|byte[] STAsBinary())| 返回 Geography 实例的开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式。 此值不包含该实例传递的任何 Z 或 M 值。
|byte[] serialize()| 返回表示 Geography 类型的内部 SQL Server 格式的字节。
|布尔 hasM()| 返回对象是否包含 M （度量） 值。
|布尔 hasZ()| 返回对象是否包含 Z （标高） 值。
|Double getLatitude()| 返回的纬度值。
|Double getLongitude()| 返回经度值。
|Double getM()| 返回的对象的 M （度量） 值。
|Double getZ()| 返回的对象的 Z （标高） 值。
|int getSrid()| 返回的空间引用标识符 (SRID) 值。
|boolean isNull()| 返回的 Geography 对象是否为 null。
|int STNumPoints()| 返回的 Geography 对象中的点数。
|String STGeographyType()| 返回由地域实例表示的开放地理空间联盟 (OGC) 类型名称。
|String asTextZM()| 返回的 Geography 对象的熟知文本 (WKT) 表示形式。
|字符串 tostring （)| 返回的 Geography 对象的字符串表示形式。

## <a name="limitations-of-spatial-datatypes"></a>空间数据类型的限制

1. 空间子数据类型**CircularString**， **CompoundCurve**， **CurvePolygon**，以及**FullGlobe**开始仅支持从 SQL Server 2012 及更高版本。

2. 始终加密不能用于空间数据类型。

3. 存储过程、 TVP 和 BulkCopy 操作当前不支持使用空间数据类型。

## <a name="see-also"></a>另请参阅

[空间数据类型示例 (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
