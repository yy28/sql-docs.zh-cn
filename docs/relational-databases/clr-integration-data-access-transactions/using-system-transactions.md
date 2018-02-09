---
title: "使用 System.Transactions |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 28edabefb40a43db17bb69a484c97e2c55f64274
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**System.Transactions**命名空间提供与 ADO.NET 完全集成的事务框架和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言运行时 (CLR) 集成。 **System.Transactions.TransactionScope**类，使代码块事务通过隐式登记的分布式事务中的连接。 必须调用**完成**末尾的代码块的方法标记**TransactionScope**。 **释放**当程序执行离开代码块，导致要如果停用的事务调用方法**完成**不调用方法。 如果已引发导致代码离开范围的异常，则将该事务视为停止使用。  
  
 我们建议你采用**使用**块以确保**释放**方法调用**TransactionScope**对象时**使用**退出块。 如果无法提交或回滚挂起的事务可能会严重降低由于性能的默认超时为**TransactionScope**一分钟。 如果不使用**使用**语句中，你必须执行中的所有工作**重**阻止和显式调用**释放**中的方法**最后**块。  
  
 如果某个中发生异常**TransactionScope**，事务将标记为不一致并被弃用。 它将会回滚当**TransactionScope**已释放。 如果未发生异常，则提交参与的事务。  
  
 **TransactionScope**仅在访问本地和远程数据源或外部的资源管理器时，才应使用。 这是因为**TransactionScope**始终导致事务要升级，即使它正在使用仅在上下文连接。  
  
> [!NOTE]  
>  **TransactionScope**类创建的事务**System.Transactions.Transaction.IsolationLevel**的**Serializable**默认情况下。 根据您的应用程序，您可能希望考虑降低隔离级别，以避免在应用程序中发生争用激烈的情况。  
  
> [!NOTE]  
>  建议您在分布式事务内针对远程服务器仅执行更新、插入和删除操作，因为这些操作占用大量数据库资源。 如果将在本地服务器上执行该操作，则不需要分布式事务，而使用本地事务。 SELECT 语句可能会不必要地锁定数据库资源，在某些情况下，可能必须使用事务进行选择。 应在事务范围之外执行任何非数据库工作，除非它涉及其他事务资源管理器。 尽管事务范围内的异常会使事务无法提交，但是**TransactionScope**类具有没有规定回滚任何更改你的代码所作的事务范围之外本身。 如果你需要采取某项操作，事务回滚时，你必须编写您自己的实现**System.Transactions.IEnlistmentNotification**接口，并显式在事务中登记。  
  
## <a name="example"></a>示例  
 若要使用**System.Transactions**，你必须具有对 System.Transactions.dll 文件的引用。  
  
 下面的代码演示如何创建可根据两个不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行提升的事务。 这些实例都由两个不同**System.Data.SqlClient.SqlConnection**对象，包装在**TransactionScope**块。 该代码创建**TransactionScope**块**使用**语句，并打开第一个连接，自动登记在**TransactionScope**。 该事务最初作为轻型事务登记，而不是完全分布式事务。 代码假定存在条件逻辑（为简洁起见，已省略该逻辑）。 仅当需要打开第二个连接登记在**TransactionScope**。 打开该连接后，事务将自动提升为完全分布式事务。 然后，则代码调用**TransactionScope.Complete**，其中提交事务。 退出时，代码将释放的两个连接**使用**语句的连接。 **TransactionScope.Dispose**方法**TransactionScope**的终止时自动调用**使用**阻止**TransactionScope**。 如果在任意位置引发异常**TransactionScope**块，**完成**功能不会调用，以及将回滚分布式的事务当**TransactionScope**已释放。  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成和事务](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
