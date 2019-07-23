---
title: registerOutParameter 方法 (int, int, int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d902d4e0-881f-4182-814c-0ede9a8da7fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6948bf6b86160b1752a483b13f83abbfc467ef2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975941"
---
# <a name="registeroutparameter-method-int-int-int"></a>registerOutParameter 方法 (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定序号位置的 OUT 参数注册为给定的 JDBC 类型和小数位数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 int scale)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 一个 int 值，此值指示参数的序号位置  。  
  
 *sqlType*  
  
 在 java.sql.Types 中定义的 JDBC 类型代码。  
  
 *scale*  
  
 一个 int 值，此值指示要放在小数点右边的位数  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 registerOutParameter 方法由 registerOutParameter 方法在 CallableStatement 接口中指定。  
  
 从 JDBC Driver 3.0 开始, 当*sqlType*的类型为**sendTimeAsDatetime**时, 此方法的行为由连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 修改, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 有关详细信息, 请参阅[配置如何将 .Java 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [registerOutParameter 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
