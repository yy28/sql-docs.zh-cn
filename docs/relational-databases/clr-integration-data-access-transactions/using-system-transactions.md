---
title: 使用系统.事务 |微软文档
description: System.事务命名空间提供了一个与ADO.NET和 SQL Server CLR 集成完全集成的事务框架。
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
ms.openlocfilehash: 7fa98e9e13062d358a6a1810485d45c8d9d3e911
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488482"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.事务**命名空间提供了一个事务框架，该框架与ADO.NET和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通用语言运行时 （CLR） 集成完全集成。 **系统.事务.事务范围**类通过在分布式事务中隐式登记连接来创建代码块事务。 您必须在**事务作用域**标记的代码块的末尾调用**Complete**方法。 当程序执行离开代码块时调用**Dispose**方法，如果不调用**Complete**方法，则导致事务停止。 如果已引发导致代码离开范围的异常，则将该事务视为停止使用。  
  
 我们建议您使用**using**块，以确保在退出**使用**块时在**事务范围**对象上调用**Dispose**方法。 无法提交或回滚挂起的事务可能会严重降低性能，因为**事务范围**的默认超时为一分钟。 如果不使用**using**语句，则必须在**Try**块中执行所有工作，并在**Finally**块中显式调用**Dispose**方法。  
  
 如果**事务范围内**发生异常，则事务将标记为不一致并放弃。 释放**事务范围**时回滚它。 如果未发生异常，则提交参与的事务。  
  
 仅当访问本地和远程数据源或外部资源管理器时，才应使用**事务范围**。 这是因为**事务范围**总是导致事务升级，即使它仅在上下文连接中使用也是如此。  
  
> [!NOTE]  
>  **默认情况下，事务范围**类创建具有**System.事务.事务.隔离级别的****事务**。 根据您的应用程序，您可能希望考虑降低隔离级别，以避免在应用程序中发生争用激烈的情况。  
  
> [!NOTE]  
>  建议您在分布式事务内针对远程服务器仅执行更新、插入和删除操作，因为这些操作占用大量数据库资源。 如果将在本地服务器上执行该操作，则不需要分布式事务，而使用本地事务。 SELECT 语句可能会不必要地锁定数据库资源，在某些情况下，可能必须使用事务进行选择。 应在事务范围之外执行任何非数据库工作，除非它涉及其他事务资源管理器。 尽管事务范围内的异常阻止事务提交，但**事务范围**类没有用于回滚代码在事务本身范围之外所做的任何更改的规定。 如果在回滚事务时需要执行一些操作，则必须编写自己的**System.事务.IEnlistment 通知**接口，并在事务中显式登记。  
  
## <a name="example"></a>示例  
 要使用**System.事务**，您必须具有对 System.事务.dll 文件的引用。  
  
 下面的代码演示如何创建可根据两个不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行提升的事务。 这些实例由两个不同的**System.Data.SqlClient.SqlConnect**对象表示，它们包在**事务范围**块中。 代码使用**using**语句创建**事务范围**块，并打开第一个连接，该连接会自动在**事务作用域**中登记它。 该事务最初作为轻型事务登记，而不是完全分布式事务。 代码假定存在条件逻辑（为简洁起见，已省略该逻辑）。 它仅在需要时才打开第二个连接，在**事务作用域**中登记它。 打开该连接后，事务将自动提升为完全分布式事务。 然后，代码调用**事务范围.Complete**，提交事务。 当退出连接的**using**语句时，代码会释放两个连接。 **事务范围**的**事务范围.Dispose**方法在**事务范围****的 using**块终止时自动调用。 如果在 **"事务范围"** 块中的任何点引发异常，则不会调用 **"完成"，** 并且分布式事务将在释放**事务范围**时回滚。  
  
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
  
  
