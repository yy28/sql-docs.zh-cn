---
title: "使用 JDBC 驱动程序管理结果设置 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e17e39f8a83313a60b269fed82631b80f07ffed5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>通过 JDBC 驱动程序管理结果集
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  结果集是一个对象，表示从数据源返回的一组数据，通常是查询的结果。 结果集包含一些行和列，用于保存请求的数据元素，并使用游标对其进行导航。 结果集是可更新的，这意味着可以对其进行修改，并将修改内容传给原始数据源。 结果集还可以有多种针对基础数据源中更改的敏感度级别。  
  
 结果集的类型确定创建一条语句时，它在调用时才[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)使类。 结果集的基本作用是向 Java 应用程序提供数据库数据的可用表示形式。 通常通过针对结果集数据元素并且带类型的 getter 和 setter 方法来完成这项任务。  
  
 在下面的示例中，后者基于[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中，通过调用创建一个结果集[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 从结果集中的数据然后通过使用显示[getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 本部分中的主题说明结果集用法的各个方面，包括游标类型、并发和行锁定。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[了解游标类型](../../connect/jdbc/understanding-cursor-types.md)|描述了不同游标类型[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持。|  
|[了解并发控制](../../connect/jdbc/understanding-concurrency-control.md)|说明 JDBC 驱动程序如何支持并发控制。|  
|[了解行锁定](../../connect/jdbc/understanding-row-locking.md)|说明 JDBC 驱动程序如何支持行锁定。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

