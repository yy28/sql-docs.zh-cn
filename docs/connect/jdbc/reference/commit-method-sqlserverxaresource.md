---
title: commit 方法 (SQLServerXAResource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerXAResource.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d0f8612-fb4a-4eca-bc37-8342e1419fd4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c6bdb28d36a148cab744fe5d9b0dbe321998757
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="commit-method-sqlserverxaresource"></a>commit 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提交全局给定的 Xid 对象所指定的事务。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void commit(javax.transaction.xa.Xid xid,  
                   boolean onePhase)  
```  
  
#### <a name="parameters"></a>Parameters  
 *xid*  
  
 Xid 对象。  
  
 *onePhase*  
  
 一个布尔值。  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>注释  
 由 javax.transaction.xa.XAResource 接口中的提交方法指定此 commit 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
