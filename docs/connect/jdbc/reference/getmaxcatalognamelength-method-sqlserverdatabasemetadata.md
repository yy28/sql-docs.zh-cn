---
title: getMaxCatalogNameLength 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxCatalogNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 89c11327-eae1-4178-9e26-4b484d521c65
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ccd38f36f9ad009c433672c8a5d522eae61aa886
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811755"
---
# <a name="getmaxcatalognamelength-method-sqlserverdatabasemetadata"></a>getMaxCatalogNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在目录名称中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxCatalogNameLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxCatalogNameLength 方法由 java.sql.DatabaseMetaData 接口中的 getMaxCatalogNameLength 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
