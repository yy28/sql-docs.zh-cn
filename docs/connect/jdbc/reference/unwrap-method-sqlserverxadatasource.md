---
title: unwrap 方法 (SQLServerXADataSource) |Microsoft 文档
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
ms.assetid: d97c99b3-2224-4abb-8b32-40aff49fe759
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 596495feb1845a43d3748a5594a708b9d9fed767
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="unwrap-method-sqlserverxadatasource"></a>unwrap 方法 (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个实现指定的接口，以允许访问的对象[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parameters  
 *iface*  
  
 类型的类**T**定义的接口。  
  
## <a name="return-value"></a>返回值  
 实现指定接口的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 [Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)由 java.sql.Wrapper 接口，在引入 JDBC 4.0 规范中定义方法。  
  
 应用程序可能需要访问特定于 JDBC API 扩展[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 Unwrap 方法支持解包到此对象扩展的公共类，如果类公开供应商扩展。  
  
 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)类扩展[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)类，该类从扩展[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)类。 当调用此方法时，该对象解包到以下类： [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，和[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXADataSource 方法](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 成员](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 类](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
