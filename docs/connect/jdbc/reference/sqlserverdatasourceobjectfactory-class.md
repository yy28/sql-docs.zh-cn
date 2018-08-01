---
title: SQLServerDataSourceObjectFactory 类 |Microsoft Docs
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38046845"
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
  
## <a name="remarks"></a>Remarks  
 所有的数据源类都继承此方法。 作为对可引用接口的支持的一部分，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 公开了实现 ObjectFactory 的此类。 Java 应用程序服务器将在数据源类上调用 getReference，这将创建一个在内部将类名用作类工厂的 Reference 对象。  
  
 当 Java 应用程序服务器必须取消引用引用对象时，它创建 SQLServerDataSourceObjectFactory 对象和调用的实例[getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md)方法，为传入引用对象，检索的数据源实例。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSourceObjectFactory 成员](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
