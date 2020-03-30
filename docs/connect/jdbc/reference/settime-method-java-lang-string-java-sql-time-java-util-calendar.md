---
title: 设置时间和日历值的 setTime 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTime (java.lang.String, java.lang.Time, java.lang.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca08fea8-ee1a-49e4-a973-2923d325df79
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e0a493492c581150809fee6e3707cf770960462
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972531"
---
# <a name="settime-method-javalangstring-javasqltime-javautilcalendar"></a>setTime 方法 (java.lang.String, java.sql.Time, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的时间和日历值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTime(java.lang.String sCol,  
                    java.sql.Time x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *x*  
  
 Time 对象。  
  
 *c*  
  
 Calendar 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setTime 方法是由 java.sql.CallableStatement 接口中的 setTime 方法指定的。  
  
 自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 驱动程序 3.0 起，此方法的行为由 sendTimeAsDatetime  连接属性（[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)）和 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 修改。  
  
 有关详细信息，请参阅[配置将 java.sql.Time 值发送到服务器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setTime 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
