---
description: SQLServerException 构造函数 (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
title: SQLServerException 构造函数 (java.lang.Object, java.lang.String, java.lang.String, int, boolean) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f66bd8759733c2574438ba12ce9f12b00cf88842
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450475"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException 构造函数 (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  当 object**** 对象、string**** 对象、string**** 对象、int**** 和 boolean**** 给定时，初始化 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 类的新实例。

## <a name="syntax"></a>语法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>参数  
 *obj*  
  
 生成了异常的 IO 缓冲区。

 *errText*  
  
 包含错误文本的字符串。
  
 *sqlState*  
  
 包含 SQL 状态的枚举对象。
 
 errNum**  
  
 包含异常的错误代码的 int。
 
 bStack**  
  
 指明是否应生成堆栈跟踪的 boolean。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
