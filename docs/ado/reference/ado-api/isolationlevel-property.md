---
title: IsolationLevel 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e027e325ec27bf5a80cf4df85afcfe59656ce3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697584"
---
# <a name="isolationlevel-property"></a>IsolationLevel 属性
指示隔离级别[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)值。 默认值是**adXactReadCommitted**。  
  
## <a name="remarks"></a>备注  
 使用**IsolationLevel**属性来设置隔离级别**连接**对象。 设置下一次调用之前不会生效[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您请求的隔离级别不可用，提供程序可能返回下一更高级别的隔离，而不更新**IsolationLevel**属性。  
  
 **IsolationLevel**属性为读/写。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**连接**对象， **IsolationLevel**可以将属性设置为仅**adXactUnspecified**。 由于用户正在使用断开连接**记录集**对象上的客户端缓存，可能有多用户的问题。 例如，当两个不同的用户尝试更新同一条记录，远程数据服务只是允许的用户首次更新的记录以"win。 第二个用户的更新请求会失败并出现错误。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [IsolationLevel 和 Mode 属性示例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 属性示例 （VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
