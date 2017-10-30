---
title: "setClientInfo 方法 （java.lang.String，java.lang.String） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b464cc1e1f63612557d6358f40b6c45cafc726e5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setclientinfo-method-javalangstring-javalangstring"></a>setClientInfo 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置指定客户端信息属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setClientInfo (java.lang.String name,  
                           java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
  
 包含要设置的客户端信息属性的名称的字符串。  
  
 *值*  
  
 包含要将客户端信息属性设置为的值的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 setClientInfo 方法指定此 setClientInfo 方法。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]不支持任何客户端信息属性。 在 2.0 JDBC 驱动程序中，此方法生成属性的警告。 应用程序应使用[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)类检索一条警告。  
  
## <a name="see-also"></a>另请参阅  
 [setClientInfo 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

