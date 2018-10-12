---
title: getObjectInstance 方法 (SQLServerDataSourceObjectFactory) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aab186f41d494e9bddf7885ddf7d9f7b3ff65972
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849497"
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
 ref  
  
 Object 值。  
  
 *名称*  
  
 对象的名称。  
  
 *c*  
  
 相对指定名称的上下文。  
  
 h  
  
 创建对象时使用的环境。  
  
## <a name="return-value"></a>返回值  
 Object 值。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此 getObjectInstance 方法由 javax.naming.spi.ObjectFactory 接口中的 getObjectInstance 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSourceObjectFactory 方法](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory 成员](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory 类](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
