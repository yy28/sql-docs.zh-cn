---
title: "isWrapperFor 方法 (SQLServerCallableStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 71156863-3588-453e-b5a5-0573b2c1bebf
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f9dbbea767628235a468cb595b7e4a74068a41a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="iswrapperfor-method-sqlservercallablestatement"></a>isWrapperFor 方法 (SQLServerCallableStatement)
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
 [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)方法和[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)方法定义由 java.sql.Wrapper 接口，在 JDBC 4.0 中引入。  
  
 如果此方法返回**true**，则调用[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)用同一参数将会成功。  
  
 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [unwrap 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
