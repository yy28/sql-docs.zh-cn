---
title: getObjectInstance 方法 (SQLServerDataSourceObjectFactory) |Microsoft 文档
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
ms.topic: article
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38ed185d36188d4889ee35e9188aa907324c9038
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>getObjectInstance 方法 (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定数据源对象的实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>Parameters  
 *ref*  
  
 **对象**值。  
  
 *名称*  
  
 对象的名称。  
  
 *C*  
  
 相对指定名称的上下文。  
  
 *H*  
  
 创建对象时使用的环境。  
  
## <a name="return-value"></a>返回值  
 **对象**值。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 javax.naming.spi.ObjectFactory 接口中的 getObjectInstance 方法指定此 getObjectInstance 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSourceObjectFactory 方法](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory 成员](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory 类](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
