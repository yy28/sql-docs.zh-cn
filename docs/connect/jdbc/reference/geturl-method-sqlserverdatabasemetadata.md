---
title: getURL 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49d8f8b4cd8b88cdf7fad86a0c09aed5792bdf81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>getURL 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库的 URL。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**包含的 URL。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getURL 方法指定此 getURL 方法。  
  
 使用时[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，此方法返回**字符串**值，该值包含以下信息：  
  
-   "jdbc:sqlserver://" 的 URL 值  
  
-   可选的连接属性，如**serverName**， **instanceName**，和**端口号**  
  
-   其他连接属性设置按用户和所有连接具有非空或非 null 的驱动程序的属性默认值除外**用户名**，**密码**，和**integratedSecurity**.  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
