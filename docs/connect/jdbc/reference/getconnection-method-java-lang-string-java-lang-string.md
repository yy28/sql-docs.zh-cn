---
title: getConnection 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 86c6637a3f502212b2b2f35a47207d7276ce8df5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763291"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定的用户名和密码尝试与此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象表示的数据源建立连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parameters  
 *username*  
  
 一个包含用户名的字符串  。  
  
 password   
  
 一个包含密码的字符串  。  
  
## <a name="return-value"></a>返回值  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此 getConnection 方法由 javax.sql.DataSource 接口中的 getConnection 方法指定。  
  
 调用 getConnection 方法替换非 null 的用户名或密码将替换初始化 SQLServerConnection 对象时在 SQLServerDataSource 类设置的用户名称和密码属性。 例如，如果调用方对数据源调用了 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 和 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)，然后调用 getConnection 并提供非 Null 的用户名或非 Null 的密码，则由 setUser 和 setPassword 设置的用户名和密码将被替换为传入 getConnection 的用户名和密码。  
  
> [!NOTE]  
>  在这种情况下，通过调用 [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) 方法在 URL 中设置的用户名和密码将保持不变。  
  
## <a name="see-also"></a>另请参阅  
 [getConnection 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
