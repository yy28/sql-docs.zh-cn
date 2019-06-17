---
title: getReference 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 50eace66b5f792ce9876d56dab8768555a43392f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775604"
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回对此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象的引用。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>返回值  
 引用对象。  
  
## <a name="remarks"></a>Remarks  
 此 getReference 方法由 javax.naming.Referenceable 接口中的 getReference 方法指定。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 之前，如果对 SQLServerDataSource 对象调用 SQLServerDataSource.setTrustStorePassword，密码将会出现在 SQLServerDataSource.getReference 所返回的对象中，从而能够使用此对象建立其他的连接。 在 JDBC Driver 3.0 中，您在使用 SQLServerDataSource.getReference 返回的对象建立连接前，将需要设置该对象的密码。  
  
 而且，如果您在绑定数据源属性前设置 SQLServerDataSource.setTrustStorePassword，在获取连接前必须调用 SQLServerDataSource.setTrustStorePassword。 例如，  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
