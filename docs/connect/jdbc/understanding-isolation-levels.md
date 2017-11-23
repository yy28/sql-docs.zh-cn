---
title: "了解隔离级别 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5acd91539652aefd7eee0049bb2e1ccc277c16a0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-isolation-levels"></a>了解隔离级别
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  事务指定一个隔离级别，该隔离级别定义一个事务必须与其他事务所进行的资源或数据更改相隔离的程度。 隔离级别从允许的并发副作用（例如，脏读或虚拟读取）的角度进行描述。  
  
 事务隔离级别控制以下各项：  
  
-   读取数据时是否占用锁以及所请求的锁类型。  
  
-   占用读取锁的时间。  
  
-   引用其他事务修改的行的读取操作是否：  
  
    -   在该行上的排他锁被释放之前阻塞其他事务。  
  
    -   检索在启动语句或事务时存在的行的已提交版本。  
  
    -   读取未提交的数据修改。  
  
 选择事务隔离级别不影响为保护数据修改而获取的锁。 事务始终获取其修改并保存，该锁直到完成事务，而不考虑设置该事务的隔离级别的任何数据上的排他锁。 对于读取操作，事务隔离级别主要定义保护级别，以防受到其他事务所做更改的影响。  
  
 较低的隔离级别会增加多个用户能够一次访问数据，但会增加的并发效果，例如脏读或丢失的更新，用户可能会遇到的数目。 相反，较高的隔离级别减少了用户可能遇到的并发副作用的类型，但需要更多的系统资源，并增加了一个事务阻塞其他事务的可能性。 应平衡应用程序的数据完整性要求与每个隔离级别的开销，在此基础上选择相应的隔离级别。 最高隔离级别（可序列化）保证事务在每次重复读取操作时都能准确检索到相同的数据，但需要通过执行某种级别的锁定来完成此操作，而锁定可能会影响多用户系统中的其他用户。 最低隔离级别（未提交读）可以检索其他事务已经修改、但未提交的数据。 在未提交读中，所有并发副作用都可能发生，但因为没有读取锁定或版本控制，所以开销最少。  
  
## <a name="remarks"></a>注释  
 下表显示了不同隔离级别允许的并发副作用。  
  
|隔离级别|脏读|不可重复读|虚拟读取|  
|---------------------|----------------|-------------------------|-------------|  
|未提交读|是|是|是|  
|已提交读|是|是|是|  
|可重复读|是|是|是|  
|Snapshot|是|“否”|是|  
|可序列化|是|“否”|是|  
  
 事务必须至少在可重复读的隔离级别运行，才能在两个事务都检索同一行，然后根据原先检索的值更新行时，防止出现丢失更新的情况。 如果两个事务使用一个 UPDATE 语句更新行，而且更新并不以先前检索的值为基础，则在默认的已提交读的隔离级别上不会发生丢失更新的情况。  
  
 若要设置事务的隔离级别，你可以使用[setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 此方法接受**int**作为其参数，如以下所示的连接常量之一基于的值：  
  
```  
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```  
  
 若要使用新的快照隔离级别的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可以使用如下的 SQLServerConnection 常量之一：  
  
```  
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```  
  
 或者，您可以使用：  
  
```  
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```  
  
 有关详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]隔离级别，请参阅"中的隔离级别[!INCLUDE[ssDE](../../includes/ssde_md.md)]"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
