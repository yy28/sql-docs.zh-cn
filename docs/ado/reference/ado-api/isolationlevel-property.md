---
title: "IsolationLevel 属性 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Connection15::IsolationLevel
helpviewer_keywords: IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f9b94c3d33c04f71adbbf82c9a4aa672d04fc482
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="isolationlevel-property"></a>IsolationLevel 属性
指示的隔离级别[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)值。 默认值是**adXactReadCommitted**。  
  
## <a name="remarks"></a>Remarks  
 使用**IsolationLevel**属性来设置的隔离级别的**连接**对象。 设置直到下次调用的时不会生效[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您请求的隔离级别不可用，提供程序可能返回下一个更大的隔离级别，而无需更新**IsolationLevel**属性。  
  
 **IsolationLevel**属性为读/写。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**连接**对象， **IsolationLevel**属性可以将仅为**adXactUnspecified**。 由于用户正在使用断开连接**记录集**对象对客户端缓存，可能有多用户的问题。 例如，当两个不同的用户尝试更新同一记录时，远程数据服务只允许的用户首次更新记录以"win。 第二个用户的更新请求将失败并出错。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [IsolationLevel 和模式属性示例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和模式属性示例 （VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
