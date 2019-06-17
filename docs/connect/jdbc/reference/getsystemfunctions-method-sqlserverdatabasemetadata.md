---
title: getSystemFunctions 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSystemFunctions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d390ec5-9ee2-49c4-b661-a93b55691dd1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0176be5707f0e0af9fa2444445881eed3039d532
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802615"
---
# <a name="getsystemfunctions-method-sqlserverdatabasemetadata"></a>getSystemFunctions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可用于此数据库的系统函数的以逗号分隔的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSystemFunctions()  
```  
  
## <a name="return-value"></a>返回值  
 包含系统函数列表的 String  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSystemFunctions 方法由 java.sql.DatabaseMetaData 接口中的 getSystemFunctions 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
