---
description: ISQLServerConnection 接口
title: ISQLServerConnection 接口 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1cedc723bcaee3b8ca850d7671ea0c868f9e11fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433509"
---
# <a name="isqlserverconnection-interface"></a>ISQLServerConnection 接口
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示连接到 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的 JDBC 连接。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此接口。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.sql.Connection  
  
## <a name="syntax"></a>语法  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>备注  
 此接口由 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)实现。  
  
 此接口公开以下 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的字段：  
  
|字段|有关详细信息，请参阅|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
