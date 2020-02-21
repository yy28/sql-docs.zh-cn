---
title: 通过 JDBC 驱动程序管理结果集 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 273a03e088036057f6d7b31c98074391138de07e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027914"
---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>通过 JDBC 驱动程序管理结果集
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  结果集是一个对象，表示从数据源返回的一组数据，通常是查询的结果。 结果集包含一些行和列，用于保存请求的数据元素，并使用游标对其进行导航。 结果集是可更新的，这意味着可以对其进行修改，并将修改内容传给原始数据源。 结果集还可以有多种针对基础数据源中更改的敏感度级别。  
  
 创建语句时（即在调用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法时）确定结果集的类型。 结果集的基本作用是向 Java 应用程序提供数据库数据的可用表示形式。 通常通过针对结果集数据元素并且带类型的 getter 和 setter 方法来完成这项任务。  
  
 以下示例基于 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库，通过调用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法创建结果集。 然后使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 方法显示结果集中的数据。  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 本部分中的主题说明结果集用法的各个方面，包括游标类型、并发和行锁定。  
  
## <a name="in-this-section"></a>在本节中  
  
|主题|说明|  
|-----------|-----------------|  
|[了解游标类型](../../connect/jdbc/understanding-cursor-types.md)|说明 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持的不同游标类型。|  
|[了解并发控制](../../connect/jdbc/understanding-concurrency-control.md)|说明 JDBC 驱动程序如何支持并发控制。|  
|[了解行锁](../../connect/jdbc/understanding-row-locking.md)|说明 JDBC 驱动程序如何支持行锁定。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
