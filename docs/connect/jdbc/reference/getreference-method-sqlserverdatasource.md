---
title: getReference 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b35f7ea76e51327bd6e4605fad28aa5f29e79b16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回对此引用[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>返回值  
 引用对象。  
  
## <a name="remarks"></a>注释  
 由 javax.naming.Referenceable 接口中的 getReference 方法指定此 getReference 方法。  
  
 之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0，如果对 SQLServerDataSource 对象，在调用 SQLServerDataSource.setTrustStorePassword 密码也会在出现 SQLServerDataSource.getReference，允许可用于对象返回的对象建立其他连接。 在 JDBC Driver 3.0 中，您在使用 SQLServerDataSource.getReference 返回的对象建立连接前，将需要设置该对象的密码。  
  
 而且，如果您在绑定数据源属性前设置 SQLServerDataSource.setTrustStorePassword，在获取连接前必须调用 SQLServerDataSource.setTrustStorePassword。 例如：  
  
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
  
  
