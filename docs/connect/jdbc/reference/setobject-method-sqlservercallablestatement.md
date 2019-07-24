---
title: setObject 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7110f6c5-4af3-4b50-a4d4-1bae1876c70d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdd1912a04c503b59064a0e39859a5845c4c6b0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973303"
---
# <a name="setobject-method-sqlservercallablestatement"></a>setObject 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定对象设置指定参数的值。  
  
 从 JDBC Driver 3.0 开始, 此方法的行为由 sendTimeAsDatetime 连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)修改。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
 有关详细信息, 请参阅[配置如何将 .Java 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>重载列表  
  
|“属性”|描述|  
|----------|-----------------|  
|[setObject (java.lang.String, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object.md)|使用给定对象设置指定参数的值。|  
|[setObject (java.lang.String, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int.md)|使用给定的对象和目标类型设置指定参数的值。|  
|[setObject (java.lang.String, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int-int.md)|使用给定的对象、目标类型和小数位数设置指定参数的值。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
