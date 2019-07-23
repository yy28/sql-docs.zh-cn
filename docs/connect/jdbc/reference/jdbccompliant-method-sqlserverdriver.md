---
title: jdbcCompliant 方法 (SQLServerDriver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c36d7980355eed1e1a1e8f42fb53c75fdb70d0ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976957"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>jdbcCompliant 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  验证 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 是否符合 JDBC 规范。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>返回值  
 如果 JDBC Driver 符合最低要求，则为 true  。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 此 jdbcCompliant 方法由 jdbcCompliant 方法在 java .sql 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成员](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 类](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
