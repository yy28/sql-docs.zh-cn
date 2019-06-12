---
title: rollback 方法 (java.sql.Savepoint) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback (java.sql.Savepoint)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d5dbd9ef-194f-4130-bfcc-7901a4fa8ded
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f5d3aff96e90dd5de4e283697084ab0614d12f05
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765518"
---
# <a name="rollback-method-javasqlsavepoint"></a>rollback 方法 (java.sql.Savepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  撤消在设置给定 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 对象后所做的所有更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void rollback(java.sql.Savepoint s)  
```  
  
#### <a name="parameters"></a>Parameters  
 *s*  
  
 回滚到保存点对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此回退方法由 java.sql.Connection 接口中的 rollBack 方法指定。  
  
 仅当已禁用自动提交模式时才应使用此方法。  
  
## <a name="see-also"></a>另请参阅  
 [rollback 方法&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
