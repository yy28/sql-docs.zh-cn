---
title: setObject 方法 (java.lang.String, java.lang.Object, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject (java.lang.String, java.lang.Object, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16f5f09a-51b5-423a-b52d-8c2eaa04e9ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31e42f5f4f0a165dd15a072f38bc158b939f74a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973357"
---
# <a name="setobject-method-javalangstring-javalangobject-int-int"></a>setObject 方法 (java.lang.String, java.lang.Object, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定的对象、目标类型和小数位数设置指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o,  
                      int n,  
                      int m)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *o*  
  
 Object 值  。  
  
 *n*  
  
 一个 int 值，此值指示 java.sql.Types 中定义的目标类型  。  
  
 *m*  
  
 指示小数点右边的位数的 int  。 对于除 NUMERIC 和 DECIMAL 外的其他类型，忽略此参数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setObject 方法是由 java.sql.CallableStatement 接口中的 setObject 方法指定的。  
  
 从 JDBC Driver 3.0 开始, 此方法的行为由 sendTimeAsDatetime 连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)修改。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
 有关详细信息, 请参阅[配置如何将 .Java 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setObject 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
