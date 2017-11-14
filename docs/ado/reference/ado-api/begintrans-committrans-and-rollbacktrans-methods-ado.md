---
title: "BeginTrans、 CommitTrans 和不方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e973503fcdd7a524bab21364428be6b955017af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans、 CommitTrans 和不方法 (ADO)
这些事务方法管理在内部处理的事务[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，如下所示：  
  
-   **BeginTrans**开始新事务。  
  
-   **CommitTrans**保存任何更改并结束当前事务。 它还可能会启动一个新的事务。  
  
-   **如果不**取消当前事务过程中做出任何更改并结束事务。 它还可能会启动一个新的事务。  
  
## <a name="syntax"></a>语法  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>返回值  
 **BeginTrans**可以作为返回的函数调用**长**变量，用于指示事务的嵌套级别。  
  
#### <a name="parameters"></a>Parameters  
 *对象*  
 A**连接**对象。  
  
## <a name="connection"></a>连接  
 使用这些方法与**连接**对象时你想要保存或取消的一系列的源数据作为单个单元进行的更改。 例如，若要将帐户之间的资金，你中减去一个金额从一个并添加到其他相同的量。 如果任一更新失败，帐户将无法再平衡。 打开的事务中进行这些更改可确保所有或任何更改都。  
  
> [!NOTE]
>  并非所有提供程序支持事务。 验证提供程序定义的属性"**事务 DDL**"将出现在**连接**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，，该值指示提供程序支持事务。 如果提供程序不支持事务，调用这些方法之一将返回错误。  
  
 调用后**BeginTrans**方法，该提供程序不再即时的方式将提交直到你调用所做的更改**CommitTrans**或**不**结束事务。  
  
 对于提供程序支持嵌套的事务，调用**BeginTrans**内打开的事务的方法会启动一个新的嵌套事务。 返回值指示的嵌套级别:"1"的返回值指示你已打开了顶级事务 （即，事务不嵌套在另一个事务），"2"指示打开第二个级别的事务 (事务嵌套在顶级事务），依次类推。 调用**CommitTrans**或**不**影响仅最新打开的事务; 你必须先关闭或之前可以解决任何更高级别的事务回滚当前事务。  
  
 调用**CommitTrans**方法保存连接上打开的事务中所做的更改，并结束事务。 调用**不**方法将反转在打开的事务中进行任何更改，并结束事务。 在没有任何打开的事务时才调用任何一种方法将生成错误。  
  
 具体取决于**连接**对象的[属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性，调用**CommitTrans**或**不**方法可能自动启动一个新的事务。 如果**属性**属性设置为**adXactCommitRetaining**，提供程序将自动启动新事务后的**CommitTrans**调用。 如果**属性**属性设置为**adXactAbortRetaining**，提供程序将自动启动新事务后的**不**调用。  
  
## <a name="remote-data-service"></a>远程数据服务  
 **BeginTrans**， **CommitTrans**，和**不**在客户端上没有方法的**连接**对象。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [BeginTrans、 CommitTrans，以及如果不方法示例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans、 CommitTrans 和不方法示例 （VC + +）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

