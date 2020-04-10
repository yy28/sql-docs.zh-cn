---
title: recover 方法 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b78165b8c199a04d716d18614e6fb56232eca429
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923113"
---
# <a name="recover-method-sqlserverxaresource"></a>recover 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  从资源管理器获取准备好的事务分支的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>参数  
 *flag*  
  
 int 值  ，可取下列值之一：XAResource.TMSTARTRSCAN、XAResource.TMENDRSCAN、XAResource.TMNOFLAGS 或 XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN。  
  
## <a name="return-value"></a>返回值  
 Xid 对象。  
  
## <a name="exceptions"></a>例外  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>备注  
 此 recover 方法是由 javax.transaction.xa.XAResource 接口中的 recover 方法指定的。  
  
 如果参数 flag  不是 XAResource.TMSTARTRSCAN 或 XAResource.TMSTARTRSCAN | XAResource.TMENDRSCAN，表明恢复扫描一定正在进行中。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
