---
title: "SQLServerDataSourceObjectFactory 类 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19f81b3a458ac0fa2d5e276858fcff45eeb0eb4b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverdatasourceobjectfactory-class"></a>SQLServerDataSourceObjectFactory 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示将来自 Java 命名和目录接口 (JNDI) 的数据源具体化的对象工厂。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.lang.Object  
  
 **实现：** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>注释  
 所有的数据源类都继承此方法。 作为可引用的接口，其支持的一部分[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]公开实现 ObjectFactory 此类。 Java 应用程序服务器将对数据源类中，调用 getReference，这将创建作为其类工厂在内部使用的类名的引用对象。  
  
 当 Java 应用程序服务器来取消引用对象时，它创建的 SQLServerDataSourceObjectFactory 对象并调用实例[getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md)方法，并为在引用对象中传递检索的数据源实例。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSourceObjectFactory 成员](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

