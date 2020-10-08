---
description: 使用空间数据类型
title: 使用空间数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02b545ec1d33d17674266d58a2a120f07af423ad
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727524"
---
# <a name="using-spatial-datatypes"></a>使用空间数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从 JDBC 驱动程序预览版 6.5.0 开始，支持空间数据类型（Geometry 和 Geography）。 存储过程、表值参数 (TVP)、BulkCopy 和 Always Encrypted 当前不支持空间数据类型。 本页介绍 JDBC 驱动程序提供的 Geometry 和 Geography 数据类型的各种用例。 有关空间数据类型的概述，请查看[空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)页面。

## <a name="creating-a-geometry--geography-object"></a>创建 geometry / geography 对象

创建 Geometry / Geography 对象的主要方法有两种：从熟知文本 (WKT) 或内部 SQL Server 格式 (CLR) 进行转换。

### <a name="creating-from-wkt"></a>从 WKT 创建

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

这将创建具有 Spatial Reference System Identifier (SRID) 0 的 LINESTRING Geometry 对象和具有 SRID 4326 的 Geography 对象。

### <a name="creating-from-clr"></a>从 CLR 创建

```java
byte[] geomCLR = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogCLR = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomCLR);
Geography geogWKT = Geography.deserialize(geogCLR);
```

这将创建一个 Geometry 和 Geography 对象，该对象与以前从 WKT 创建的对象相同。

## <a name="working-with-a-geometry--geography-object"></a>使用 Geometry / Geography 对象

假设用户在 SQL Server 上有如下所示的一个表：

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

插入 Geometry 值的示例脚本为：

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

使用 Geography 列和 setGeography()**** 方法可以对 Geography 对应项执行相同的操作。

要读取 Geometry / Geography 列，请执行以下操作：

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

使用 Geography 列和 getGeography()**** 方法可以对 Geography 对应项执行相同的操作。

## <a name="newly-introduced-apis"></a>新引入的 API

以下是在此新增功能中引入的新公共 API，它们位于类 SQLServerPreparedStatement****、SQLServerResultSet****、Geometry**** 和 Geography**** 中。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|说明|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 将指定参数设置为给定的 microsoft.sql.Geometry 类对象。
|void setGeography(int n, Geography x)| 将指定参数设置为给定的 microsoft.sql.Geography 类对象。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|说明|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 返回此 ResultSet 对象的当前行中指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geometry 对象。
|Geometry getGeometry(String columnName)| 返回此 ResultSet 对象的当前行中指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geometry 对象。
|Geography getGeography(int colunIndex)| 返回此 ResultSet 对象的当前行中指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geography 对象。
|Geography getGeography(String columnName)| 返回此 ResultSet 对象的当前行中指定列的值作为 Java 编程语言中的 com.microsoft.sqlserver.jdbc.Geography 对象。

### <a name="geometry"></a>几何结构

|方法|说明|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geometry 实例的构造函数，增加了该实例传递的任何 Z（标高）和 M（度量）值。
|Geometry STGeomFromWKB(byte[] wkb)| 开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式的 Geometry 实例的构造函数。 注意：此方法目前使用内部 SQL Server 格式 (CLR) 来创建 Geometry 实例，这是驱动程序中的一个已知问题，计划将其更改为接受 WKB 数据。 对于已经使用此方法的现有用户，请考虑切换为 deserialize(byte)。
|Geometries deserialize(byte[] clr)| 空间数据的内部 SQL Server 格式的 Geometry 实例的构造函数。
|Geometry parse(String wkt)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geometry 实例的构造函数。 空间引用标识符默认为 0。
|Geometry point(double x, double y, int SRID)| Geometry 实例的构造函数，表示来自其 X 和 Y 值的 Point 实例以及空间引用标识符。
|String STAsText()| 返回 Geometry 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
|byte[] STAsBinary()| 返回 Geometry 实例的内部 SQL Server 格式 (CLR) 表示形式。 此值不包含该实例传递的任何 Z 或 M 值。
|byte[] serialize()| 返回表示 Geometry 类型的内部 SQL Server 格式的字节。
|boolean hasM()| 如果对象包含 M（度量）值，则返回。
|boolean hasZ()| 如果对象包含 Z（标高）值，则返回。
|Double getX()| 返回 X 坐标值。
|Double getY()| 返回 Y 坐标值。
|Double getM()| 返回对象的 M（度量）值。
|Double getZ()| 返回对象的 Z（标高）值。
|int getSrid()| 返回空间引用标识符 (SRID) 值。
|boolean isNull()| 如果 Geometry 对象为 null，则返回。
|int STNumPoints()| 返回 Geometry 对象的点数。
|String STGeometryType()| 返回由几何图形实例表示的开放地理空间联盟 (OGC) 类型名称。
|String asTextZM()| 返回 Geometry 对象的熟知文本 (WKT) 表示形式。
|String toString()| 返回 Geometry 对象的字符串表示形式。

### <a name="geography"></a>地理位置

|方法|说明|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geography 实例的构造函数，增加了该实例传递的任何 Z（标高）和 M（度量）值。
|Geography STGeomFromWKB(byte[] wkb)| 开放地理空间信息联盟 (OGC) 熟知二进制 (WKB) 表示形式的 Geography 实例的构造函数。 注意：此方法目前使用内部 SQL Server 格式 (CLR) 来创建 Geometry 实例，但在将来将改为接受 WKB 数据，因为此方法 (STGeomFromWKB) 的对应 SQL Server 使用 WKB。 对于已经使用此方法的现有用户，请考虑切换为 deserialize(byte)。
|Geography deserialize(byte[] clr)| 空间数据的内部 SQL Server 格式的 Geography 实例的构造函数。
|Geography parse(String wkt)| 开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式的 Geography 实例的构造函数。 空间引用标识符默认为 0。
|Geography point(double lon, double lat, int SRID)| 地理实例的构造函数，它表示来自其经纬度的点实例和空间引用标识符。
|String STAsText()| 返回 Geography 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。
|byte[] STAsBinary())| 返回 Geography 实例的内部 SQL Server 格式 (CLR) 表示形式。 此值不包含该实例传递的任何 Z 或 M 值。
|byte[] serialize()| 返回表示 Geography 类型的内部 SQL Server 格式的字节。
|boolean hasM()| 如果对象包含 M（度量）值，则返回。
|boolean hasZ()| 如果对象包含 Z（标高）值，则返回。
|Double getLatitude()| 返回纬度值。
|Double getLongitude()| 返回经度值。
|Double getM()| 返回对象的 M（度量）值。
|Double getZ()| 返回对象的 Z（标高）值。
|int getSrid()| 返回空间引用标识符 (SRID) 值。
|boolean isNull()| 如果 Geography 对象为 null，则返回。
|int STNumPoints()| 返回 Geography 对象的点数。
|String STGeographyType()| 返回由地域实例表示的开放地理空间联盟 (OGC) 类型名称。
|String asTextZM()| 返回 Geography 对象的熟知文本 (WKT) 表示形式。
|String toString()| 返回 Geography 对象的字符串表示形式。

## <a name="limitations-of-spatial-datatypes"></a>空间数据类型的限制

1. 从 SQL Server 2012 及更高版本开始，仅支持空间子数据类型 CircularString****、CompoundCurve****、CurvePolygon**** 和 FullGlobe****。

2. Always Encrypted 不能与空间数据类型一起使用。

3. 当前，空间数据类型不支持存储过程、TVP 和 BulkCopy 操作。

## <a name="see-also"></a>另请参阅

[空间数据类型示例 (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)