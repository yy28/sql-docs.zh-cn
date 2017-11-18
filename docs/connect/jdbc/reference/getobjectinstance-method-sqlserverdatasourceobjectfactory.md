---
title: "getObjectInstance 方法 (SQLServerDataSourceObjectFactory) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d560f49aeb499c304028b3f2b317b2cb790faaa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

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
  
 *c*  
  
 相对指定名称的上下文。  
  
 *h*  
  
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
  
  

