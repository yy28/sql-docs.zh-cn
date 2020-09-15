---
description: SQLServerConnectionPoolDataSource 类
title: SQLServerConnectionPoolDataSource 类 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2faa9b4df512d9b37bbba581353938120b85cbb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354783"
---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示用于连接池管理器的物理数据库连接。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **实现：** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>备注  
 SQLServerConnectionPoolDataSource 通常用于 Java 应用程序服务器环境中，此环境支持内置连接池并需要 ConnectionPoolDataSource 提供物理连接，例如可以提供 JDBC 3.0 API 规范连接池的 Java Platform、Enterprise Edition (Java EE) 应用程序服务器。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnectionPoolDataSource 成员](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
