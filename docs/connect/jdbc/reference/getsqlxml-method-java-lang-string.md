---
title: "getSQLXML 方法 (java.lang.String) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f56b192a-3255-4215-b552-8e494fbca083
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 21eba6572ba201ae68891cf2c80545d586903290
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlxml-method-javalangstring"></a>getSQLXML 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  作为给定参数名称 SQLXML 对象中检索指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *参数名称*  
  
 A**字符串**，该值指示参数名称。  
  
## <a name="return-value"></a>返回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getSQLXML 方法指定此 getSQLXML 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getSQLXML 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

