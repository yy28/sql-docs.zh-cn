---
title: getHoldability 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57bf0cfc206319bf6afcb09435e8787499266c0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982922"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的可保持性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>返回值  
 包含下列可保持性级别之一的 int  值：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getHoldability 方法由 getHoldability 方法在方法中指定。  
  
 若要设置结果集可保持性，应用程序可使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法。 调用 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法、创建语句对象及其结果集对象并执行该语句后，应用程序可能需要再次更改可保持性。  
  
 对于服务器游标，当连接到 SQL Server 2005 或更高版本时，设置可保持性只会影响该连接上将要创建的新结果集的可保持性。 但是，如果使用 SQL Server 2000，设置保持能力会影响该连接上现有的结果集和将要创建的新结果集的保持能力。  
  
 当重置保持能力并对先前创建的结果集对象调用 getHoldability 方法时, 此方法返回的值可能与以下方法返回的保持能力值不同:。 getResultSetHoldability、GetHoldability 或 Java.sql.databasemetadata。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
