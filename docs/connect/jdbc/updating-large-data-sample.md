---
title: 更新大型数据的示例 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 231125f60ec0c5791e55a10cff56b3b93339fb91
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027069"
---
# <a name="updating-large-data-sample"></a>更新大型数据的示例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 示例应用程序说明了如何更新数据库中的大型列。

此示例的代码文件名为 UpdateLargeData.java，该文件可在以下位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>要求

要运行此示例应用程序，将需要访问 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库。 还必须将 classpath 设置为包含 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 若要详细了解如何设置类路径，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供四个类库文件：sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 此示例使用 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 和 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法，这两个方法是在 JDBC 4.0 API 中引入的，用于访问特定于驱动程序的响应缓冲方法。 为了编译和运行此示例，您需要对 JDBC 4.0 提供支持的 sqljdbc4.jar 类库。 有关选择哪个 JAR 文件的详细信息，请参阅 [JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>示例

在下面的示例中，示例代码建立与 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 数据库的连接。 接下来，示例代码创建一个 Statement 对象并使用 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 方法来检查 Statement 对象是否是指定的 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的包装。 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法用于访问特定于驱动程序的响应缓冲方法。

接下来，示例代码使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法将响应缓冲模式设置为“adaptive”，并演示如何获取自适应缓冲模式。

然后，它运行 SQL 语句，并将返回的数据放入可更新的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中。

最后，示例代码将循环访问结果集中的数据行。 如果找到空的文档摘要，将结合使用 [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 和 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法来更新数据行，并再次将它保存到数据库中。 如果已有数据，将使用 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 方法来显示部分数据。

驱动程序的默认行为是“adaptive”  。 但是，对于只进的可更新结果集，以及当结果集中的数据大于应用程序内存时，应用程序必须使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法显式设置自适应缓冲模式。

[!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>另请参阅

[处理大型数据](../../connect/jdbc/working-with-large-data.md)
