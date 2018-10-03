---
title: getSQLKeywords 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLKeywords
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a2a0dfbb-11ec-429f-aea6-8f44148ebb8e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3010ba1e7c846f7da859fdf35ccef20b63e02aa3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660355"
---
# <a name="getsqlkeywords-method-sqlserverdatabasemetadata"></a>getSQLKeywords 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库的所有 SQL 关键字（但并非 SQL92 关键字）的以逗号分隔的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSQLKeywords()  
```  
  
## <a name="return-value"></a>返回值  
 一个**字符串**，其中包含 SQL 关键字。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSQLKeywords 方法由 java.sql.DatabaseMetaData 接口中的 getSQLKeywords 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
