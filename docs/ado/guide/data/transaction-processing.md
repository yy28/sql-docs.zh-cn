---
title: 事务处理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ea890e0e2d49781f06f38f606a6c92582dc44d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472186"
---
# <a name="transaction-processing"></a>事务处理
一个*事务*分隔的开头和结尾的一系列通过连接执行的数据访问操作。 视您的数据源，事务性功能而定**连接**对象还允许您创建和管理事务。 例如，使用 Microsoft OLE DB Provider for SQL Server 访问 Microsoft SQL Server 上的数据库，您可以创建多个嵌套的事务执行的命令。  
  
 ADO 可确保对在事务中的操作生成的数据源的更改已成功在一起或根本不会发生。  
  
 如果取消该事务，或如果其中一个操作失败，结果将是因为如果未在事务中的操作发生。 事务开始前将一直保持数据源。  
  
 ADO 提供了以下用于控制事务的方法：**BeginTrans**， **CommitTrans**，和**RollbackTrans**。 使用这些方法与**连接**时想要保存或取消对作为单个单元的源数据所做更改的一系列对象。 例如，若要帐户之间转移资金，您从一个的金额中减去并将相同的量添加到另。 如果任一更新失败，帐户将无法再平衡。 打开的事务中进行这些更改可确保所有或任何更改都。  
  
> [!NOTE]
>  并非所有提供程序支持的事务。 验证提供程序定义的属性"**事务 DDL**"将出现在**连接**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，表示提供程序支持事务。 如果提供程序不支持事务，调用这些方法之一，将返回错误。  
  
 调用后**BeginTrans**方法，该提供程序将无法再在瞬间完成提交在您调用之前所做的更改**CommitTrans**或**RollbackTrans**结束事务。  
  
 调用**CommitTrans**方法保存的连接上打开的事务中所做的更改并结束事务。 调用**RollbackTrans**方法反转任何打开的事务中所做的更改并结束事务。 在没有任何打开的事务时调用任一种方法将生成错误。  
  
 具体取决于**连接**对象的[特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性，调用**CommitTrans**或者**RollbackTrans**方法可能自动启动新事务。 如果**特性**属性设置为**adXactCommitRetaining**，该提供程序会自动启动后的一个新事务**CommitTrans**调用。 如果**特性**属性设置为**adXactAbortRetaining**，该提供程序会自动启动后的一个新事务**RollbackTrans**调用。  
  
## <a name="transaction-isolation-level"></a>事务隔离级别  
 使用**IsolationLevel**属性上设置事务的隔离级别**连接**对象。 设置下一次调用之前不会生效[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您请求的隔离级别不可用，则提供程序可能返回下一更高级别的隔离。 请参阅**IsolationLevel**上有效的值的更多详细信息的 ADO 程序员参考中的属性。  
  
## <a name="nested-transactions"></a>嵌套的事务  
 对于提供程序支持嵌套的事务，调用**BeginTrans**中打开的事务的方法将启动一个新的嵌套事务。 返回值指示的嵌套级别:"1"的返回值指示已打开顶级事务 （即事务不嵌套在另一个事务），"2"指示是否已打开第二个级别的事务 (事务嵌套在顶级事务），依次类推。 调用**CommitTrans**或**RollbackTrans**影响仅最新打开的事务; 您必须关闭或之前可以解决任何更高级别的事务回滚当前事务。
