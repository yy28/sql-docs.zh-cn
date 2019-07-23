---
title: supportsOpenStatementsAcrossRollback 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOpenStatementsAcrossRollback
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4e38b938-f39f-4c5d-9b32-4ba489535c45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ea2ba789b3b2d34671f07acad9f5a7e6636326c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969065"
---
# <a name="supportsopenstatementsacrossrollback-method-sqlserverdatabasemetadata"></a>supportsOpenStatementsAcrossRollback 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持回滚时保持打开语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsOpenStatementsAcrossRollback()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持,**则为 true** 。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 supportsOpenStatementsAcrossRollback 方法由 supportsOpenStatementsAcrossRollback 方法在 Java.sql.databasemetadata 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
