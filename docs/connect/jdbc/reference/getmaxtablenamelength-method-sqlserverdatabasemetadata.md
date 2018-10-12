---
title: getMaxTableNameLength 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxTableNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5c51218f-c6e8-49f4-ad09-292e849ca43a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c92624d88142e4b4e1909acd298e4ed439d57d6d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819725"
---
# <a name="getmaxtablenamelength-method-sqlserverdatabasemetadata"></a>getMaxTableNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在表名中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxTableNameLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxTableNameLength 方法由 java.sql.DatabaseMetaData 接口中的 getMaxTableNameLength 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
