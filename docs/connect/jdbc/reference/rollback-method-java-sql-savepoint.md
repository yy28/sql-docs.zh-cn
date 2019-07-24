---
title: rollback 方法 (.sql) |Microsoft Docs
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
ms.openlocfilehash: f4aad09c11a3003a286e27ecd144cefc22e4bb9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975728"
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
  
 要回滚到的保存点对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此回滚方法由 sql 中的 rollBack 方法指定。  
  
 仅当已禁用自动提交模式时才应使用此方法。  
  
## <a name="see-also"></a>另请参阅  
 [rollback 方法&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
