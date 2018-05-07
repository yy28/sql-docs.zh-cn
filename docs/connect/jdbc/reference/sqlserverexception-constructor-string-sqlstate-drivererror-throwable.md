---
title: SQLServerException 构造函数 (java.lang.String，SQLState，DriverError，java.lang.Throwable) |Microsoft 文档
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
ms.openlocfilehash: 33f7b15a2f4dd8e83c7e703e96812f29691e6bd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>SQLServerException 构造函数 (java.lang.String，SQLState，DriverError，java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)类在给定**字符串**对象， **sqlstate**对象， **drivererror**对象，和一个**可引发**对象。

## <a name="syntax"></a>语法  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parameters  
 *errText*  
  
 一个字符串，包含错误文本。
  
 *sqlState*  
  
 一个用于保存 SQL 状态的枚举对象。
 
 *driverError*  
  
 保存驱动程序错误的枚举对象。
 
 *可能的原因*  
  
 包含导致异常的可引发对象。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
