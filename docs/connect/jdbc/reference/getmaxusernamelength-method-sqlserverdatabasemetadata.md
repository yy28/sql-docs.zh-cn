---
title: getMaxUserNameLength 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxUserNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 09ec7d40-4c4a-4d89-ba11-78e5327b5759
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76e42e523dbd883dfd7c8b95c59687b1c91a8260
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743007"
---
# <a name="getmaxusernamelength-method-sqlserverdatabasemetadata"></a>getMaxUserNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在用户名中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxUserNameLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxUserNameLength 方法由 java.sql.DatabaseMetaData 接口中的 getMaxUserNameLength 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
