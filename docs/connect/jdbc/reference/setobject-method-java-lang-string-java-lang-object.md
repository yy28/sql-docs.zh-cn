---
title: "setObject 方法 （java.lang.String，java.lang.Object） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.setObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 14b84409-5510-4642-a83b-732d8511c5b1
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 572d4b53bca44d51f4e6c9f41c6d16be40aeaeea
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setobject-method-javalangstring-javalangobject"></a>setObject 方法 (java.lang.String, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置使用给定的对象的指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 A**字符串**，其中包含参数名称。  
  
 *o*  
  
 **对象**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 setObject 方法指定此 setObject 方法。  
  
 如果在将参数发送到数据库前给出了 NULL，此方法会将指定的参数转换为 CHAR。 如果将参数声明为 binary、varbinary 或 image SQL 类型，则在执行语句时会引发异常。  
  
 开头[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0，此方法的行为来修改**sendTimeAsDatetime**连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setObject 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
