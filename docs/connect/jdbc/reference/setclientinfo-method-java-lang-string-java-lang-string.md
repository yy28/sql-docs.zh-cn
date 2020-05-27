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
ms.openlocfilehash: b94f6a00e26934426ef1ece760ce1179c3c53046
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "76941175"
---
# <a name="setclientinfo-method-javalangstring-javalangstring"></a>setClientInfo 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置指定客户端信息属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setClientInfo (java.lang.String name,  
                           java.lang.String value)  
```  
  
#### <a name="parameters"></a>parameters  
 name   
  
 包含要设置的客户端信息属性名称的 String。  
  
 *value*  
  
 包含客户端信息属性设置值的 String。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setClientInfo 方法是由 java.sql.Connection 接口中的 setClientInfo 方法指定的。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 不支持任何客户端信息属性。 在 2.0 JDBC 驱动程序中，此方法生成属性的警告。 应用程序应使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 的 [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) 方法来检索警告。  
  
## <a name="see-also"></a>另请参阅  
 [setClientInfo 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
