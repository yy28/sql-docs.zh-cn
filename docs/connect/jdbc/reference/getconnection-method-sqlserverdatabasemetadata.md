---
title: getConnection 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getConnection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16e46603-a678-4b0f-998e-479abbea151c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bc564a941994f9b9ce4305d52e71cfba987f080
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690265"
---
# <a name="getconnection-method-sqlserverdatabasemetadata"></a>getConnection 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索生成此元数据对象的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>返回值  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getConnection 方法由 java.sql.DatabaseMetaData 接口中的 getConnection 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
