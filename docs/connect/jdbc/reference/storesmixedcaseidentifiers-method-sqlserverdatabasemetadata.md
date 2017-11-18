---
title: "storesMixedCaseIdentifiers 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.storesMixedCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a91e5cd6-22b1-464e-aeec-665590737a74
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33c36261b8f5c8ec935f6b61ebd533f8c30bd039
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="storesmixedcaseidentifiers-method-sqlserverdatabasemetadata"></a>storesMixedCaseIdentifiers 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否将未用双引号引起来的大小写混合的 SQL 标识符视为不区分大小写，并以混合大小写方式存储它们。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean storesMixedCaseIdentifiers()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果标识符存储在混合大小写。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 storesMixedCaseIdentifiers 方法指定此 storesMixedCaseIdentifiers 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

