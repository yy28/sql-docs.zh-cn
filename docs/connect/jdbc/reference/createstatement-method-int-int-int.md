---
title: "createStatement 方法 （int、 int、 int） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0298571db91e5f733de531f1ff30de88c457b5f7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="createstatement-method-int-int-int"></a>createStatement 方法 (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，它生成[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)具有给定的类型、 并发和保持能力的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>Parameters  
 *resultSetType*  
  
 **Int**表示结果的值设置类型。  
  
 *nConcur*  
  
 **Int**表示结果的值设置并发类型。  
  
 *nHold*  
  
 **Int**值，该值表示保持能力。  
  
## <a name="return-value"></a>返回值  
 语句对象中。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 createStatement 方法指定此 createStatement 方法。  
  
## <a name="see-also"></a>另请参阅  
 [createStatement 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
