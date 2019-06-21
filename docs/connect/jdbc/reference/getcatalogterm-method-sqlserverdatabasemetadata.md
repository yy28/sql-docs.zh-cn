---
title: getCatalogTerm 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0aa5d372-16aa-4790-a8f6-f8b742798f8f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9a99453f869167a3804643baac750cf91dd82266
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796793"
---
# <a name="getcatalogterm-method-sqlserverdatabasemetadata"></a>getCatalogTerm 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索数据库供应商有关“目录”的首选术语。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalogTerm()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含目录术语的 String  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCatalogTerm 方法是由 java.sql.DatabaseMetaData 接口中的 getCatalogTerm 方法指定的。  
  
 将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库一起使用时，此方法将返回术语“数据库”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
