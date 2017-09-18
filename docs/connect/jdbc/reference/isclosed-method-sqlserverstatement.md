---
title: "关闭方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e79b5b53-16b0-42a3-be4e-542a77a21e12
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fdd47545dcf4962eca79dc764b03f63f72d20343
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="isclosed-method-sqlserverstatement"></a>isClosed 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示是否这[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象已关闭。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象已关闭， **false**如果它仍处于打开状态。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的关闭方法指定此关闭方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
