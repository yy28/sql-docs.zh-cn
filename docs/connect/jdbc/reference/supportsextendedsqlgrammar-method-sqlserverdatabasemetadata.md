---
title: supportsExtendedSQLGrammar 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsExtendedSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8deb1987-c4e3-4599-8e37-0a04ec20b480
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f006c4343c1a89fcb6387bc437a3415607ca094
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969417"
---
# <a name="supportsextendedsqlgrammar-method-sqlserverdatabasemetadata"></a>supportsExtendedSQLGrammar 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持 ODBC 扩展的 SQL 语法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsExtendedSQLGrammar()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsExtendedSQLGrammer 方法是由 java.sql.DatabaseMetaData 接口中的 supportsExtendedSQLGrammer 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
