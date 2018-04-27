---
title: isWrapperFor 方法 (SQLServerDataSource) |Microsoft 文档
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
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b687a5d3f05484eb906e14773dd0b519d387215
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="iswrapperfor-method-sqlserverdatasource"></a>isWrapperFor 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此数据源对象是否为指定接口的包装。  
  
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
 [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)方法和[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)方法定义由 java.sql.Wrapper 接口，在 JDBC 4.0 规范中引入。  
  
 如果此方法返回 true，则调用[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)用同一参数将会成功。  
  
 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [unwrap 方法&#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
