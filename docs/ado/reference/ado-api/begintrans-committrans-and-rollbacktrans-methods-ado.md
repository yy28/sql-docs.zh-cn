---
title: BeginTrans、 CommitTrans 和 RollbackTrans 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ee5560a27f7df49a82e964753f792bd46270d3a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696491"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)
这些事务方法管理事务中处理[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，如下所示：  
  
-   **BeginTrans**开始新事务。  
  
-   **CommitTrans**保存任何更改并结束当前事务。 它还可能会启动新事务。  
  
-   **RollbackTrans**取消在当前事务期间所做的任何更改并结束事务。 它还可能会启动新事务。  
  
## <a name="syntax"></a>语法  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>返回值  
 **BeginTrans**可作为返回的函数调用**长**变量，用于指示事务的嵌套级别。  
  
#### <a name="parameters"></a>Parameters  
 *object*  
 一个**连接**对象。  
  
## <a name="connection"></a>连接  
 使用这些方法与**连接**时想要保存或取消对作为单个单元的源数据所做更改的一系列对象。 例如，若要帐户之间转移资金，您从一个的金额中减去并将相同的量添加到另。 如果任一更新失败，帐户将无法再平衡。 打开的事务中进行这些更改可确保所有或任何更改都。  
  
> [!NOTE]
>  并非所有提供程序支持的事务。 验证提供程序定义的属性"**事务 DDL**"将出现在**连接**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，表示提供程序支持事务。 如果提供程序不支持事务，调用这些方法之一，将返回错误。  
  
 调用后**BeginTrans**方法，该提供程序将无法再在瞬间完成提交在您调用之前所做的更改**CommitTrans**或**RollbackTrans**结束事务。  
  
 对于提供程序支持嵌套的事务，调用**BeginTrans**中打开的事务的方法将启动一个新的嵌套事务。 返回值指示的嵌套级别:"1"的返回值指示已打开顶级事务 （即事务不嵌套在另一个事务），"2"指示是否已打开第二个级别的事务 (事务嵌套在顶级事务），依次类推。 调用**CommitTrans**或**RollbackTrans**影响仅最新打开的事务; 您必须关闭或之前可以解决任何更高级别的事务回滚当前事务。  
  
 调用**CommitTrans**方法保存的连接上打开的事务中所做的更改并结束事务。 调用**RollbackTrans**方法反转任何打开的事务中所做的更改并结束事务。 在没有任何打开的事务时调用任一种方法将生成错误。  
  
 具体取决于**连接**对象的[特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性，调用**CommitTrans**或者**RollbackTrans**方法可能自动启动新事务。 如果**特性**属性设置为**adXactCommitRetaining**，该提供程序会自动启动后的一个新事务**CommitTrans**调用。 如果**特性**属性设置为**adXactAbortRetaining**，该提供程序会自动启动后的一个新事务**RollbackTrans**调用。  
  
## <a name="remote-data-service"></a>远程数据服务  
 **BeginTrans**， **CommitTrans**，并**RollbackTrans**方法不可用客户端上**连接**对象。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法示例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法示例 （VC + +）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
