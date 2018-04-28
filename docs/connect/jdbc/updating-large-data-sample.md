---
title: 更新较大的数据示例 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c385a868346f1b574e05b2be38dfd70d239cec27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updating-large-data-sample"></a>更新大型数据的示例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]示例应用程序演示如何更新数据库中的大型列。  
  
 此示例的代码文件名为 updateLargeData.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\adaptive  
  
## <a name="requirements"></a>需求  
 若要运行此示例应用程序，你将需要访问[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 还必须将 classpath 设置为包含 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供了具体取决于你首选的 Java Runtime Environment (JRE) 设置要使用的 sqljdbc.jar、 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 类库文件。 此示例使用[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)和[unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) JDBC 4.0 API，以访问特定于驱动程序的响应缓冲方法中引入的方法。 为了编译和运行此示例，您需要对 JDBC 4.0 提供支持的 sqljdbc4.jar 类库。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码建立连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]数据库。 然后，示例代码创建语句对象并使用[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)方法检查语句对象是否为指定的包装器[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 [Unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)方法可用来访问特定于驱动程序的响应缓冲方法。  
  
 接下来，示例代码设置响应缓冲模式下"**自适应**"使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类以及演示如何获取自适应缓冲模式。  
  
 然后，它运行 SQL 语句中，并将放到可更新它返回的数据[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
 最后，示例代码将循环访问结果集中包含的数据行。 如果找到一个空的文档摘要，它使用的组合[updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)和[updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法来更新数据行并再次将其保留到数据库。 如果已存在数据，它将使用[getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)方法以显示一些，它包含的数据。  
  
 该驱动程序的默认行为是"**自适应。**" 但是，对于只进的可更新结果集和结果集中的数据大于应用程序内存时，应用程序必须通过使用显式设置的自适应缓冲模式[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法的[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。  
  
 [!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [处理大型数据](../../connect/jdbc/working-with-large-data.md)  
  
  
