---
title: getSendTimeAsDatetime 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a105e66b346c130a1d310aab153cf4e78ced0d95
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784683"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此方法。  
  
 返回的设置**sendTimeAsDatetime**连接属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果将 java.sql.Time 值发送到与服务器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime**类型。 **false**如果将 java.sql.Time 值发送到与服务器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**时间**类型。  
  
## <a name="remarks"></a>Remarks  
 请参阅[连接属性设置](../../../connect/jdbc/setting-the-connection-properties.md)有关详细信息**sendTimeAsDatetime**连接属性。  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 使你能够以编程方式设置“sendTimeAsDatetime”连接属性。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
