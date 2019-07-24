---
title: getMaxRowSize 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxRowSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abb5a204-76ff-4381-ab2b-896a19b202f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b261a0f02075ffea736899dfa941a4e9f5acfb86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982042"
---
# <a name="getmaxrowsize-method-sqlserverdatabasemetadata"></a>getMaxRowSize 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在单行中允许的最大字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxRowSize()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字节数的 int  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxRowSize 方法由 getMaxRowSize 方法在 Java.sql.databasemetadata 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
