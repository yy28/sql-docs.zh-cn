---
title: 读取较大的数据示例 |Microsoft 文档
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
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1898eb29b5c2e335fa355b43d8037ba9b4b2c910
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="reading-large-data-sample"></a>读取大型数据的示例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]示例应用程序演示如何检索从较大的单列值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]通过使用数据库[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)方法。  
  
 此示例的代码文件名为 readLargeData.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\adaptive  
  
## <a name="requirements"></a>需求  
 若要运行此示例应用程序，你将需要访问[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。 还必须将 classpath 设置为包含 sqljdbc.jar 文件或 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc.jar 项或 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 类库文件，以便根据你首选的 Java Runtime Environment (JRE) 设置来使用。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码建立连接[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]数据库。 接下来，示例代码创建示例数据并使用参数化查询更新 Production.Document 表。  
  
 此外，示例代码演示如何使用获取自适应缓冲模式[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)类。 请注意，从 JDBC Driver 2.0 发行版开始，responseBuffering 连接属性默认情况下设置为“adaptive”。  
  
 然后，使用的 SQL 语句[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，示例代码运行 SQL 语句，并把它将返回到该数据放[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
 最后，示例代码循环访问的结果集中包含的数据行，并使用[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)方法来访问某些，它包含的数据。  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [处理大型数据](../../../connect/jdbc/working-with-large-data.md)  
  
  
