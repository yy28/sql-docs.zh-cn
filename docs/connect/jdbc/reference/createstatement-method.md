---
title: createStatement 方法 （) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a36cae30e7a32b6045756eabb76d8d55daf2f030
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658785"
---
# <a name="createstatement-method-"></a>createStatement 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建用于将 SQL 语句发送到数据库的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Statement createStatement()  
```  
  
## <a name="return-value"></a>返回值  
 将语句对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 createStatement 方法由 java.sql.Connection 接口中的 createStatement 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [createStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
