---
title: createStatement 方法 （int，int，int） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d07029a2f076c4342c715ac6c9fac38325d1a9a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666055"
---
# <a name="createstatement-method-int-int-int"></a>createStatement 方法 (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象，该对象使用给定的类型、并发机制和可保持性生成 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>Parameters  
 *resultSetType*  
  
 **Int**值，该值表示结果集类型。  
  
 *nConcur*  
  
 表示结果集并发类型的 int 值。  
  
 *nHold*  
  
 表示可保持性的 int 值。  
  
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
  
  
