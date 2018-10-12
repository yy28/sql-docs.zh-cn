---
title: SQLServerException 构造函数 （java.lang.Object，java.lang.String，java.lang.String，int，boolean 类型的值） |Microsoft Docs
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
ms.openlocfilehash: 5b8c39021b8afac5631e44cddd8874cbf22975a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670025"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException 构造函数 （java.lang.Object，java.lang.String，java.lang.String，int，boolean 类型的值）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)类在给定**对象**即**字符串**对象，**字符串**对象、 **int**，和一个**布尔**。

## <a name="syntax"></a>语法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parameters  
 obj  
  
 IO 缓冲区生成了异常。

 *errText*  
  
 包含错误文本的字符串。
  
 *sqlState*  
  
 一个包含 SQL 状态的枚举对象。
 
 *errNum*  
  
 一个整数，它包含异常的错误代码。
 
 *bStack*  
  
 一个布尔值，该值指示是否应生成堆栈跟踪。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
