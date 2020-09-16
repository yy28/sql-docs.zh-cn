---
description: jdbcCompliant 方法 (SQLServerDriver)
title: jdbcCompliant 方法 (SQLServerDriver) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25495005dafdc95982b2f7005c96eb186c864caf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433279"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>jdbcCompliant 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  验证 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 是否符合 JDBC 规范。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>返回值  
 如果 JDBC Driver 符合最低要求，则为 true****。 否则为 **false**。  
  
## <a name="remarks"></a>备注  
 此 jdbcCompliant 方法是由 java.sql.Driver 接口中的 jdbcCompliant 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成员](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 类](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
