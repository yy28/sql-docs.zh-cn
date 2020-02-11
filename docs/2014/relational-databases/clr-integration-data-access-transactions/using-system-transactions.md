---
title: 使用 system.exception |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e39106ea1c4077d1aee90cedc17c5af07503a136
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919538"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
  
  `System.Transactions` 命名空间提供与 ADO.NET 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成完全集成的新事务框架。 
  `System.Transactions.TransactionScope` 类通过在分布式事务中隐式登记连接，使代码块成为事务代码。 您必须在 `Complete` 标记的代码块的末尾调用 `TransactionScope` 方法。 如果未调用 `Dispose` 方法，将在程序执行离开代码块时调用 `Complete` 方法，从而导致停止使用该事务。 如果已引发导致代码离开范围的异常，则将该事务视为停止使用。  
  
 建议您使用 `using` 块，以便确保在退出 `Dispose` 块时对 `TransactionScope` 对象调用 `using` 方法。 提交或回滚挂起事务失败可能会严重降低性能，因为 `TransactionScope` 的默认超时值为 1 分钟。 如果未使用 `using` 语句，必须在 `Try` 块中执行所有工作，并在 `Dispose` 块中显式调用 `Finally` 方法。  
  
 如果在 `TransactionScope` 内发生异常，则将该事务标记为不一致，并放弃使用该事务。 释放 `TransactionScope` 时将回滚该事务。 如果未发生异常，则提交参与的事务。  
  
 仅当正在访问本机和远程数据源或外部资源管理器时，才应使用 `TransactionScope`。 这是因为 `TransactionScope` 始终导致提升事务，即使仅在上下文连接内使用该事务也是如此。  
  
> [!NOTE]  
>  默认情况下，`TransactionScope` 类创建 `System.Transactions.Transaction.IsolationLevel` 为 `Serializable` 的事务。 根据您的应用程序，您可能希望考虑降低隔离级别，以避免在应用程序中发生争用激烈的情况。  
  
> [!NOTE]  
>  建议您在分布式事务内针对远程服务器仅执行更新、插入和删除操作，因为这些操作占用大量数据库资源。 如果将在本地服务器上执行该操作，则不需要分布式事务，而使用本地事务。 SELECT 语句可能会不必要地锁定数据库资源，在某些情况下，可能必须使用事务进行选择。 应在事务范围之外执行任何非数据库工作，除非它涉及其他事务资源管理器。 虽然事务范围内的异常可以避免提交该事务，但是 `TransactionScope` 类无法回滚在该事务自身范围之外对代码所做的任何更改。 如果需要在事务回滚时采取某一操作，必须写入您自己的 `System.Transactions.IEnlistmentNotification` 接口实现，并在该事务中显式登记。  
  
## <a name="example"></a>示例  
 若要使用 `System.Transactions`，必须引用 System.Transactions.dll 文件。  
  
 下面的代码演示如何创建可根据两个不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行提升的事务。 这些实例由两个不同的 `System.Data.SqlClient.SqlConnection` 对象表示，它们包装在 `TransactionScope` 块中。 该代码创建带有 `TransactionScope` 语句的 `using` 块，并打开第一个在 `TransactionScope` 中自动登记的连接。 该事务最初作为轻型事务登记，而不是完全分布式事务。 代码假定存在条件逻辑（为简洁起见，已省略该逻辑）。 代码仅在需要时打开第二个连接，并在 `TransactionScope` 中登记。 打开该连接后，事务将自动提升为完全分布式事务。 该代码随后调用 `TransactionScope.Complete`，这将提交事务。 当退出连接的 `using` 语句时，代码释放两个连接。 
  `TransactionScope.Dispose` 的 `TransactionScope` 块终止时，将自动调用 `using` 的 `TransactionScope` 方法。 如果在 `TransactionScope` 块的任一点引发异常，则不会调用 `Complete`，并且分布式事务将在释放 `TransactionScope` 时回滚。  
  
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
 [CLR 集成和事务](../native-client-ole-db-transactions/transactions.md)  
  
  
