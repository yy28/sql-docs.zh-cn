---
title: getMaxCursorNameLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxCursorNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2cd2bed9-adf4-4bcd-ae5a-d0e3428bc709
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c47f912711a486ea60cf0181411e7ed68029ab
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982147"
---
# <a name="getmaxcursornamelength-method-sqlserverdatabasemetadata"></a>getMaxCursorNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在游标名称中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxCursorNameLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getMaxCursorNameLength 方法是由 java.sql.DatabaseMetaData 接口中的 getMaxCursorNameLength 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
