---
title: supportsANSI92EntryLevelSQL 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsANSI92EntryLevelSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3fffc08-7254-4af7-bbae-8ff591fbd5ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 425174215725a2f34899731fbe97ab1b99786fba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666105"
---
# <a name="supportsansi92entrylevelsql-method-sqlserverdatabasemetadata"></a>supportsANSI92EntryLevelSQL 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持 ANSI92 入门级 SQL 语法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsANSI92EntryLevelSQL()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果受支持。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 supportsANSI92EntryLevelSQL 方法由 java.sql.DatabaseMetaData 接口中的 supportsANSI92EntryLevelSQL 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
