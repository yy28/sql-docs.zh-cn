---
title: "setCursorName 方法 (SQLServerStatement) |Microsoft 文档"
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
- SQLServerStatement.setCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3f3ec4f2-103a-4e16-9206-c5bd8639f946
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 501440dec2f47c4f3f272ebde7f6cbd01642e377
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setcursorname-method-sqlserverstatement"></a>setCursorName 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将 SQL 游标名称设置为给定字符串，该字符串将由随后的执行方法使用。  
  
> [!NOTE]  
>  此方法当前不支持通过[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 调用此方法将不起作用。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setCursorName(java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
  
 A**字符串**包含光标的名称。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 setCursorName 方法指定此 setCursorName 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

