---
title: SQLServerException 构造函数 （java.lang.Object、 java.lang.String、 java.lang.String、 int、 boolean 类型的值） |Microsoft 文档
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
ms.openlocfilehash: 7bb24e82a0c6cac43d54339652e9bfcd536482a6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845842"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException 构造函数 （java.lang.Object、 java.lang.String、 java.lang.String、 int、 boolean 类型的值）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)类在给定**对象**、**字符串**对象，**字符串**对象、 **int**，和一个**布尔**。

## <a name="syntax"></a>语法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parameters  
 *obj*  
  
 生成异常 IO 缓冲区。

 *errText*  
  
 包含错误文本的字符串。
  
 *sqlState*  
  
 一个包含 SQL 状态的枚举对象。
 
 *errNum*  
  
 一个 int，包含异常的错误代码。
 
 *bStack*  
  
 一个布尔值，该值指示是否应该生成堆栈跟踪。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
