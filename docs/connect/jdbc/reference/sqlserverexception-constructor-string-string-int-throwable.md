---
title: SQLServerException 构造函数 （java.lang.String、 java.lang.String、 int、 java.lang.Throwable） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94b45ed912fbf61a0f15b23ca5393ed31746c90b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException 构造函数 （java.lang.String、 java.lang.String、 int、 java.lang.Throwable）
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
  
 一个 int，包含异常的错误代码。
 
 *可能的原因*  
  
 一个包含异常原因的可引发对象。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
