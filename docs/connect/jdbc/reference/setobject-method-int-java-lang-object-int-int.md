---
description: setObject 方法 (int, java.lang.Object, int, int)
title: setObject 方法 (int, java.lang.Object, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d190ee20-d669-4c6f-a081-d5cfec2f72ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0dfff8bd93509a26cc499fbeeb420c8c3cdea0c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458579"
---
# <a name="setobject-method-int-javalangobject-int-int"></a>setObject 方法 (int, java.lang.Object, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定的对象、目标类型和小数位数设置指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setObject(int n,  
                            java.lang.Object obj,  
                            int targetSqlType,  
                            int scale)  
```  
  
#### <a name="parameters"></a>参数  
 *n*  
  
 指示参数编号的 int****。  
  
 *obj*  
  
 一个对象。  
  
 targetSqlType**  
  
 一个 int 值，此值指示 java.sql.Types 中定义的目标类型****。  
  
 *scale*  
  
 指示小数点右边的位数的 int****。 对于除 NUMERIC 和 DECIMAL 外的其他所有类型，忽略此参数。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setObject 方法是由 java.sql.PreparedStatement 接口中的 setObject 方法指定的。  
  
 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 开始，此方法的行为由 sendTimeAsDatetime**** 连接属性（[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)）和 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 修改。  
  
 有关详细信息，请参阅[配置将 java.sql.Time 值发送到服务器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setObject 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
