---
title: "ISQLServerConnection 接口 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 548c008a35f31f11ccd89f360541c23779dcbb82
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="isqlserverconnection-interface"></a>ISQLServerConnection 接口
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示与的 JDBC 连接[!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。 此接口已添加到中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.sql.Connection  
  
## <a name="syntax"></a>语法  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>注释  
 此接口由实现[SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)。  
  
 此接口公开以下[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定字段：  
  
|字段|有关详细信息，请参阅|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
