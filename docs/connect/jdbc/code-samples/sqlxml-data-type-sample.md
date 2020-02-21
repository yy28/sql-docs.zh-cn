---
title: SQLXML 数据类型示例 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df376535f8f6c6a7d98e1744a2d2b70e813d400a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028286"
---
# <a name="sqlxml-data-type-sample"></a>SQLXML 数据类型示例

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 示例应用程序说明如何在关系数据库中存储 XML 数据，如何从数据库中检索 XML 数据，以及如何使用 SQLXML Java 数据类型分析 XML 数据。

本部分中的代码示例使用 Simple API for XML (SAX) 分析器。 SAX 是一种公开制定的标准，用于对 XML 文档进行基于事件的分析。 它还提供了一个用于处理 XML 数据的应用程序编程接口。 请注意，应用程序也可以使用其他任何 XML 分析器，例如，文档对象模型 (DOM) 或 Streaming API for XML (StAX) 等。

文档对象模型 (DOM) 提供了 XML 文档、碎片、节点或节点集的编程表示形式。 它还提供了一个用于处理 XML 数据的应用程序编程接口。 同样，Streaming API for XML (StAX) 也是一个基于 Java 的 API，用于 XML 的拉式分析。

> [!IMPORTANT]  
> 为了使用 SAX 分析器 API，必须从 javax.xml 包导入标准的 SAX 实现。

此示例的代码文件名为 SqlXmlDataType.java，位于以下位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes
```

## <a name="requirements"></a>要求

若要运行此示例应用程序，必须将 classpath 设置为包含 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc4.jar 项，示例应用程序将引发“找不到类”异常。 若要详细了解如何设置类路径，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。

此外，还需要访问 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库才能运行此示例应用程序。

## <a name="example"></a>示例

在下面的示例中，示例代码先建立与 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 数据库的连接，然后调用 createSampleTables 方法。

如果测试表、TestTable1 和 TestTable2 存在，createSampleTables 方法会将它们删除。 然后该方法会在 TestTable1 中插入两行。

此外，代码示例还包含以下三个方法和另外一个名为 ExampleContentHandler 的类。

ExampleContentHandler 类实现一个自定义内容处理程序，该处理程序定义用于处理分析器事件的方法。

showGetters 方法演示如何使用 SAX、ContentHandler 和 XMLReader 分析 SQLXML 对象中的数据。 首先，该代码示例会创建一个自定义内容处理程序的实例，即 ExampleContentHandler。 接下来，创建和执行一个 SQL 语句，该语句从 TestTable1 返回一组数据。 然后，代码示例获取 SAX 分析器并分析 XML 数据。

showSetters 方法演示如何使用 SAX、ContentHandler 和 ResultSet 设置 xml 列。 首先，它使用 Connection 类的 [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 方法创建一个空的 SQLXML 对象。 然后，获取内容处理程序的一个实例以便向 SQLXML 对象中写入数据。 接下来，代码示例向 TestTable1 中写入数据。 最后，示例代码循环访问结果集中的数据行，并使用 [getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) 方法读取 XML 数据。

showTransformer 方法演示如何使用 SAX 和 Transformer 从一个表中获取 XML 数据，然后将该 XML 数据插入另一个表中。 首先，从 TestTable1 中检索源 SQLXML 对象。 然后，使用 Connection 类的 [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 方法创建一个空的目标 SQLXML 对象。 接下来，更新目标 SQLXML 对象，并将 XML 数据写入 TestTable2。 最后，示例代码将循环访问结果集中的数据行，并使用 [getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) 方法读取 TestTable2 中的 XML 数据。

[!code[JDBC#UsingSQLXML1](../../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]

## <a name="see-also"></a>另请参阅

[处理数据类型 &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)
