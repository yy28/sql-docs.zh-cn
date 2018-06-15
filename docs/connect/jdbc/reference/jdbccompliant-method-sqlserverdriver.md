---
title: jdbcCompliant 方法 (SQLServerDriver) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 357024153bb862ff369278096018dd544ead4ca8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32840342"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>jdbcCompliant 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  验证[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]符合 JDBC 规范。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>返回值  
 **true** JDBC 驱动程序是否满足最低要求。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 由 java.sql.Driver 接口中的 jdbcCompliant 方法指定此 jdbcCompliant 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成员](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 类](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
