---
title: "isWrapperFor 方法 (SQLServerConnectionPoolDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09ed10eb-6e46-437b-a7c0-3c55574aad38
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8025e9271a706aac4bb35bd9fd1565762632d6b9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="iswrapperfor-method-sqlserverconnectionpooldatasource"></a>isWrapperFor 方法 (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此对象是否为指定接口的包装。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parameters  
 *iface*  
  
 A**类**定义的接口。  
  
## <a name="return-value"></a>返回值  
 **true**如果此对象实现接口或包装实现接口的对象。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)方法和[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)方法定义由 java.sql.Wrapper 接口，在 JDBC 4.0 规范中引入。  
  
 如果此方法返回 true，则调用[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)用同一参数将会成功。  
  
 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [unwrap 方法 &#40;SQLServerConnectionPoolDataSource &#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成员](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 类](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

