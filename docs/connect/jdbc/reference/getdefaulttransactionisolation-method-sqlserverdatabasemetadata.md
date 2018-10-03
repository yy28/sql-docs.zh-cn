---
title: getDefaultTransactionIsolation 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDefaultTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85b867ed-de5a-4879-b3f8-bce897879077
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6c9a01c4be9dd0777d57cf87ab7613c1de3a832
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718065"
---
# <a name="getdefaulttransactionisolation-method-sqlserverdatabasemetadata"></a>getDefaultTransactionIsolation 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库的默认事务隔离级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getDefaultTransactionIsolation()  
```  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值指示默认事务隔离级别。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getDefaultTransactionIsolation 方法由 java.sql.DatabaseMetaData 接口中的 getDefaultTransactionIsolation 方法指定。  
  
 将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库一起使用时，此方法将返回 TRANSACTION_READ_COMMITTED 的值或 int 值 2。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
