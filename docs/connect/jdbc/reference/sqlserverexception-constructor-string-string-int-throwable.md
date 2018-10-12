---
title: SQLServerException 构造函数 （java.lang.String，java.lang.String，int，java.lang.Throwable） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f596056d830ae3fa3462095e5a17a112c8f641f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759255"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException 构造函数 （java.lang.String，java.lang.String，int，java.lang.Throwable）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)类在给定**字符串**对象，**字符串**对象， **int**，和**可引发**对象。

## <a name="syntax"></a>语法  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parameters  
 *errText*  
  
 包含错误文本的字符串。
  
 *errState*  
  
 包含错误的状态的字符串。
 
 *errNum*  
  
 一个整数，它包含异常的错误代码。
 
 *cause*  
  
 一个包含异常的原因可引发对象。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
