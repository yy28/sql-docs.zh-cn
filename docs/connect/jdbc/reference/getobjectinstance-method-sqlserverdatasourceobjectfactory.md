---
title: getObjectInstance 方法 (SQLServerDataSourceObjectFactory) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dac2ff8e4b88d9d8c2517cde92e7fbaaae0e2077
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925246"
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
  
#### <a name="parameters"></a>parameters  
 *ref*  
  
 Object 值  。  
  
 name   
  
 对象的名称。  
  
 *c*  
  
 相对指定名称的上下文。  
  
 h   
  
 创建对象时使用的环境。  
  
## <a name="return-value"></a>返回值  
 Object 值  。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>备注  
 此 getObjectInstance 方法是由 javax.naming.spi.ObjectFactory 接口中的 getObjectInstance 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSourceObjectFactory 方法](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory 成员](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory 类](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
