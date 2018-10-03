---
title: 读取大型数据的示例 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b2e91f5587751ca7a6d6bb7e91ab3509152b1d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645395"
---
# <a name="reading-large-data-sample"></a>读取大型数据的示例

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 示例应用程序还说明如何使用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中检索大型单列值。

此示例的代码文件名为 ReadLargeData.java，该文件可在以下位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>要求

要运行此示例应用程序，将需要访问 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库。 此外，还将 classpath 设置为包含 mssql-jdbc jar 文件。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>示例

在下面的示例中，示例代码建立与 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 数据库的连接。 接下来，示例代码创建示例数据并使用参数化查询更新 Production.Document 表。

此外，示例代码还演示如何使用 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) 方法获取自适应缓冲模式。 请注意，从 JDBC Driver 2.0 发行版开始，responseBuffering 连接属性默认情况下设置为“adaptive”。

然后，通过对 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象使用 SQL 语句，示例代码将运行此 SQL 语句并将其返回的数据放入 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中。

最后，示例代码将循环访问结果集中的数据行，并使用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法访问某些数据。

[!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>另请参阅

[处理大型数据](../../../connect/jdbc/code-samples/working-with-large-data.md)
