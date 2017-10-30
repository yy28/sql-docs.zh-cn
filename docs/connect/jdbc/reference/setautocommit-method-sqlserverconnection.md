---
title: "setAutoCommit 方法 (SQLServerConnection) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1549693ac6b4e558c2fc86b29dc6aaa6122c235
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# setAutoCommit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  此设置自动提交模式[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)到给定状态的对象。  
  
## 语法  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### Parameters  
 *值*  
  
 **true**若要启用自动提交模式连接， **false**以禁用它。  
  
## 异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## 注释  
 由 java.sql.Connection 接口中的 setAutoCommit 方法指定此 setAutoCommit 方法。  
  
 如果连接处于自动提交模式下，则其所有 SQL 语句将作为单个事务运行并提交。 否则，其 SQL 语句都分组到由调用结束的事务[提交](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)方法或[回滚](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)方法。 默认情况下，新连接处于自动提交模式。  
  
 语句执行完毕或下次运行开始时（以二者中先发生的为准）都会执行提交操作。 在返回的语句的情况下[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象，该语句完成后已检索结果集的最后一行，或已关闭结果集时。 对于更复杂的情况，单个语句可能会在输出参数值之外返回多个结果。 在这些情况下，检索完所有结果和输出参数值后将执行提交操作。  
  
 自动提交模式时**false**，JDBC 驱动程序将隐式启动每次提交后的一个新事务。  
  
> [!NOTE]  
>  如果在事务处理过程中调用此方法，将提交此事务。  
  
## 另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

