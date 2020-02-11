---
title: 使用 system.exception |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: a9b99842a92649a42e9a0a42e6732368dc5e06ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081356"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.web**命名空间提供与 ADO.NET 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言运行时（CLR）集成完全集成的事务框架。 System.exception**类通过**隐式在分布式事务中登记连接，使代码块成为事务性的。 您必须在由**TransactionScope**标记的代码块的末尾调用**完整**方法。 当程序执行离开代码块时调用**Dispose**方法，如果未调用**Complete**方法，则会导致事务中止。 如果已引发导致代码离开范围的异常，则将该事务视为停止使用。  
  
 建议你使用**using**块，以确保在退出**using**块时对**TransactionScope**对象调用**Dispose**方法。 无法提交或回滚挂起的事务可能会严重降低性能，因为**TransactionScope**的默认超时为一分钟。 如果不使用**using**语句，则必须在**Try**块中执行所有工作，并在**Finally**块中显式调用**Dispose**方法。  
  
 如果**TransactionScope**内发生异常，事务将被标记为不一致并被放弃。 在处置**TransactionScope**后，将回滚该事务。 如果未发生异常，则提交参与的事务。  
  
 仅当访问本地和远程数据源或外部资源管理器时，才应使用**TransactionScope** 。 这是因为， **TransactionScope**始终导致事务升级，即使它仅在上下文连接中使用也是如此。  
  
> [!NOTE]  
>  默认情况下， **TransactionScope**类创建具有**IsolationLevel** **的一个**事务。 根据您的应用程序，您可能希望考虑降低隔离级别，以避免在应用程序中发生争用激烈的情况。  
  
> [!NOTE]  
>  建议您在分布式事务内针对远程服务器仅执行更新、插入和删除操作，因为这些操作占用大量数据库资源。 如果将在本地服务器上执行该操作，则不需要分布式事务，而使用本地事务。 SELECT 语句可能会不必要地锁定数据库资源，在某些情况下，可能必须使用事务进行选择。 应在事务范围之外执行任何非数据库工作，除非它涉及其他事务资源管理器。 尽管事务范围内的异常会使事务无法提交，但**TransactionScope**类没有任何设置来回滚您的代码在事务本身范围之外所作的任何更改。 如果在事务回滚时需要执行某些操作，则必须编写自己的**IEnlistmentNotification**接口实现，并在事务中显式登记。  
  
## <a name="example"></a>示例  
 若要使用**system.exception，你**必须具有对 system.web .dll 文件的引用。  
  
 下面的代码演示如何创建可根据两个不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行提升的事务。 这些实例由两个不同的**SqlClient**对象表示，包装在一个**TransactionScope**块中。 此代码使用**using**语句创建**TransactionScope**块，并打开第一个连接，该连接自动在**TransactionScope**中登记。 该事务最初作为轻型事务登记，而不是完全分布式事务。 代码假定存在条件逻辑（为简洁起见，已省略该逻辑）。 它仅在需要时打开第二个连接，并在**TransactionScope**中登记它。 打开该连接后，事务将自动提升为完全分布式事务。 然后，该代码调用**TransactionScope**，并提交事务。 代码在退出用于连接的**using**语句时释放两个连接。 在**transactionscope**的**using**块终止时，将自动调用**transactionscope**的**transactionscope**方法。 如果在**transactionscope**块中的任何点引发了异常，则不会调用**Complete** ，并且释放了该**transactionscope**后，将回滚分布式事务。  
  
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
  
  
