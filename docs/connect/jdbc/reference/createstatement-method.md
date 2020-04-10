---
title: createStatement 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 480f21b6-50cc-4b1e-a0b0-8774ecfe94f1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcb82d90c030f4ebee6bd3ebae262aafb8c4e929
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927640"
---
# <a name="createstatement-method-"></a>createStatement 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建用于将 SQL 语句发送到数据库的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Statement createStatement()  
```  
  
## <a name="return-value"></a>返回值  
 Statement 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 createStatement 方法是由 java.sql.Connection 接口中的 createStatement 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [createStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
