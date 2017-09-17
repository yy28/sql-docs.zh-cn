---
title: "getClientInfo 方法 (java.lang.String) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e0f92e5db61ef0b778e293ea61b25ad61956986a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-javalangstring"></a>getClientInfo 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定客户端信息属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
  
 包含要检索的客户端信息属性的名称的字符串。  
  
## <a name="return-value"></a>返回值  
 包含客户端信息属性的值的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 getClientInfo 方法指定此 getClientInfo 方法。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]不支持任何客户端信息属性。 因此，此方法返回**null**。  
  
 同样，应用程序可以使用[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)方法[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)类检索的驱动程序支持的客户端信息属性的列表。 [GetClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)方法返回空结果集。  
  
## <a name="see-also"></a>另请参阅  
 [getClientInfo 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
