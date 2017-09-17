---
title: "getCatalogTerm 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getCatalogTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0aa5d372-16aa-4790-a8f6-f8b742798f8f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2195081eb25174092c195ac8bcfd1878c545cd8b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getcatalogterm-method-sqlserverdatabasemetadata"></a>getCatalogTerm 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索数据库供应商有关“目录”的首选术语。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalogTerm()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**，其中包含目录术语。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getCatalogTerm 方法指定此 getCatalogTerm 方法。  
  
 使用时[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，此方法将返回术语"数据库"。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
