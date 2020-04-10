---
title: setTransactionIsolation 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 165a2096a1d34152de6956b56d5273f179faf8ea
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926470"
---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  尝试将此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象的事务隔离级别更改为给定级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>parameters  
 *level*  
  
 包含下列隔离级别之一的 int  值：  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setTransactionIsolation 方法是由 java.sql.Connection 接口中的 setTransactionIsolation 方法指定的。  
  
 如果在事务中间调用此方法，将不提交事务。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
