---
title: "isWrapperFor 方法 (SQLServerPreparedStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b0e591b1-73e2-4f90-967f-5555eadfc3f1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eeab0f9a5822c53b9023181da1c4ef53cf0424bc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="iswrapperfor-method-sqlserverpreparedstatement"></a>isWrapperFor 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此语句对象是否为指定接口的包装。  
  
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
 [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)方法和[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)方法定义由 java.sql.Wrapper 接口，在 JDBC 4.0 规范中引入。  
  
 如果此方法返回 true，则调用[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)用同一参数将会成功。  
  
 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [unwrap 方法 &#40;SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

