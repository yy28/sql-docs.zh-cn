---
title: SQLServerDataSourceObjectFactory 类 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ecec8f58587d6a57468f8078e1f680675bede77
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845812"
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
  
  
