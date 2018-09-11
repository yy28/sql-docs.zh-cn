---
title: getDefaultTransactionIsolation 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
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
- SQLServerDatabaseMetaData.getDefaultTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85b867ed-de5a-4879-b3f8-bce897879077
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 406881e33395f0071f06a16df4e789c70ab95e0a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786416"
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
  
  
