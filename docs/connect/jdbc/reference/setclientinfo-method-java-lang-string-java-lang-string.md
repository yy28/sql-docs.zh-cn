---
title: setClientInfo 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ad28a2c578a4026d4152bb7056b00e8d3a05afd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667316"
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
  
 包含要设置的客户端信息属性名称的 String。  
  
 *value*  
  
 包含客户端信息属性设置值的 String。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setClientInfo 方法由 java.sql.Connection 接口中的 setClientInfo 方法指定。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 不支持任何客户端信息属性。 在 2.0 JDBC 驱动程序中，此方法生成属性的警告。 应用程序应使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 的 [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) 方法来检索警告。  
  
## <a name="see-also"></a>另请参阅  
 [setClientInfo 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
