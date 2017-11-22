---
title: "getSendTimeAsDatetime 方法 (SQLServerDataSource) |Microsoft 文档"
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
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f784b25fe9390d98d32ab31e6f3f837e30aa746b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  此方法已添加到中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0。  
  
 返回的设置**sendTimeAsDatetime**连接属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果将 java.sql.Time 值发送到与服务器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime**类型。 **false**如果将 java.sql.Time 值发送到与服务器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]**时间**类型。  
  
## <a name="remarks"></a>注释  
 请参阅[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)有关详细信息**sendTimeAsDatetime**连接属性。  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)允许你以编程方式将**sendTimeAsDatetime**连接属性。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
