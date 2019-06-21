---
title: getCatalogSeparator 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogSeparator
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0bbd6842-7210-432a-bef4-e15a63f5cc96
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d3e836a031f319c3e92227f1d51fcd436c9d3ed7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803935"
---
# <a name="getcatalogseparator-method-sqlserverdatabasemetadata"></a>getCatalogSeparator 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库用作目录和表名之间的分隔符的字符串  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalogSeparator()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含目录分隔符的字符串  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCatalogSeparator 方法是由 java.sql.DatabaseMetaData 接口中的 getCatalogSeparator 方法指定。  
  
 将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，此方法返回句点（“.”）作为目录分隔符。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
