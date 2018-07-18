---
title: 使用 System.Transactions |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e9e09ae1d55065f7f50d25c3538f3c9218d8ed52
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349799"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.Transactions**命名空间提供与 ADO.NET 完全集成的新事务框架和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言运行时 (CLR) 集成。 **System.Transactions.TransactionScope**类，使代码块事务通过隐式登记分布式事务中的连接。 必须调用**完成**代码块末尾处的方法标记为通过**TransactionScope**。 **Dispose**当程序执行离开代码块，导致如果停止该事务调用方法**完成**不会调用方法。 如果已引发导致代码离开范围的异常，则将该事务视为停止使用。  
  
 我们建议您采用**使用**块来确保**Dispose**上调用方法**TransactionScope**对象时**使用**何时退出代码块。 如果无法提交或回滚挂起的事务可能会严重降低性能由于的默认超时值**TransactionScope**为一分钟。 如果不使用**使用**语句，必须执行中的所有工作**尝试**阻止和显式调用**释放**中的方法**最后**块。  
  
 如果某个中发生异常**TransactionScope**，事务被标记为不一致并被弃用。 它将会回滚时**TransactionScope**被释放。 如果未发生异常，则提交参与的事务。  
  
 **TransactionScope**仅当要访问本地和远程数据源或外部资源管理器时，才应使用。 这是因为**TransactionScope**始终导致事务要升级，即使仅在上下文连接内正在使用它。  
  
> [!NOTE]  
>  **TransactionScope**类创建的事务**System.Transactions.Transaction.IsolationLevel**的**Serializable**默认情况下。 根据您的应用程序，您可能希望考虑降低隔离级别，以避免在应用程序中发生争用激烈的情况。  
  
> [!NOTE]  
>  建议您在分布式事务内针对远程服务器仅执行更新、插入和删除操作，因为这些操作占用大量数据库资源。 如果将在本地服务器上执行该操作，则不需要分布式事务，而使用本地事务。 SELECT 语句可能会不必要地锁定数据库资源，在某些情况下，可能必须使用事务进行选择。 应在事务范围之外执行任何非数据库工作，除非它涉及其他事务资源管理器。 事务的作用域内异常可防止事务无法提交，尽管**TransactionScope**类具有任何预配的范围之外的事务已回滚任何更改你的代码本身。 如果需要回滚事务时执行某些操作，则必须编写自己的实现**System.Transactions.IEnlistmentNotification**接口，并显式在事务中登记。  
  
## <a name="example"></a>示例  
 若要使用**System.Transactions**，必须具有对 System.Transactions.dll 文件的引用。  
  
 下面的代码演示如何创建可根据两个不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行提升的事务。 这些实例由两个不同**System.Data.SqlClient.SqlConnection**对象中包装**TransactionScope**块。 该代码会创建**TransactionScope**块**使用**语句，并打开第一个连接中, 自动登记**TransactionScope**。 该事务最初作为轻型事务登记，而不是完全分布式事务。 代码假定存在条件逻辑（为简洁起见，已省略该逻辑）。 它会打开第二个连接，仅当有必要，在登记**TransactionScope**。 打开该连接后，事务将自动提升为完全分布式事务。 然后，代码调用**TransactionScope.Complete**，这将提交事务。 退出时，代码释放两个连接的**使用**语句的连接。 **TransactionScope.Dispose**方法**TransactionScope**终止时自动调用**使用**块**TransactionScope**。 如果在任一点引发异常**TransactionScope**块中，**完成**执行不会调用和分布式的事务将会回滚时**TransactionScope**被释放。  
  
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
  
## <a name="see-also"></a>请参阅  
 [CLR 集成和事务](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
