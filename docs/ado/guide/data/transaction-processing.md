---
title: "事务处理 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a2afb43e83ebc2ed765c04fa15f070597009457
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="transaction-processing"></a>事务处理
A*事务*分隔的开头和末尾的数据访问操作通过连接执行一系列。 受制于您的数据源的事务功能**连接**对象还允许你创建和管理事务。 例如，使用 Microsoft OLE DB Provider for SQL Server 访问 Microsoft SQL Server 上的数据库，你可以创建多个嵌套的事务执行的命令。  
  
 ADO 可确保已成功在一起或根本不发生与数据源在事务中的操作而引起的更改。  
  
 如果取消该事务，或如果其中一个操作失败，结果将是如同的任何操作在事务中发生。 对事务开始之前将一直保持数据源。  
  
 ADO 提供用于控制事务的以下方法： **BeginTrans**， **CommitTrans**，和**不**。 使用这些方法与**连接**对象时你想要保存或取消的一系列的源数据作为单个单元进行的更改。 例如，若要将帐户之间的资金，你中减去一个金额从一个并添加到其他相同的量。 如果任一更新失败，帐户将无法再平衡。 打开的事务中进行这些更改可确保所有或任何更改都。  
  
> [!NOTE]
>  并非所有提供程序支持事务。 验证提供程序定义的属性"**事务 DDL**"将出现在**连接**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，，该值指示提供程序支持事务。 如果提供程序不支持事务，调用这些方法之一将返回错误。  
  
 调用后**BeginTrans**方法，该提供程序不再即时的方式将提交直到你调用所做的更改**CommitTrans**或**不**结束事务。  
  
 调用**CommitTrans**方法保存连接上打开的事务中所做的更改，并结束事务。 调用**不**方法将反转在打开的事务中进行任何更改，并结束事务。 在没有任何打开的事务时才调用任何一种方法将生成错误。  
  
 具体取决于**连接**对象的[属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性，调用**CommitTrans**或**不**方法可能自动启动一个新的事务。 如果**属性**属性设置为**adXactCommitRetaining**，提供程序将自动启动新事务后的**CommitTrans**调用。 如果**属性**属性设置为**adXactAbortRetaining**，提供程序将自动启动新事务后的**不**调用。  
  
## <a name="transaction-isolation-level"></a>事务隔离级别  
 使用**IsolationLevel**属性上设置事务的隔离级别**连接**对象。 设置直到下次调用的时不会生效[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您请求的隔离级别不可用，则提供程序可能返回下一个更大的隔离级别。 请参阅**IsolationLevel** ADO 程序员参考中为有效的值的详细信息的属性。  
  
## <a name="nested-transactions"></a>嵌套的事务  
 对于提供程序支持嵌套的事务，调用**BeginTrans**内打开的事务的方法会启动一个新的嵌套事务。 返回值指示的嵌套级别:"1"的返回值指示你已打开了顶级事务 （即，事务不嵌套在另一个事务），"2"指示打开第二个级别的事务 (事务嵌套在顶级事务），依次类推。 调用**CommitTrans**或**不**影响仅最新打开的事务; 你必须先关闭或之前可以解决任何更高级别的事务回滚当前事务。
