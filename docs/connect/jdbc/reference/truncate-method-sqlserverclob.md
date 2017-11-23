---
title: "截断方法 (SQLServerClob) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerClob.truncate
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e81d94f2539ee911bfda2b87e87676b2cebaa17a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="truncate-method-sqlserverclob"></a>truncate 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将 CLOB 截断为给定的长度。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parameters  
 *len*  
  
 CLOB 应截断为的长度（以字符数表示）。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 java.sql.Clob 接口中的截断方法指定此截断的方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
