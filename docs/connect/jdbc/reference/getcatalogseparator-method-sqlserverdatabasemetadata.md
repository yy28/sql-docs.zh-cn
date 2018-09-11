---
title: getCatalogSeparator 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogSeparator
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0bbd6842-7210-432a-bef4-e15a63f5cc96
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a8587c005186cb9806e35eec66d0ed571f372c1
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784869"
---
# <a name="getcatalogseparator-method-sqlserverdatabasemetadata"></a>getCatalogSeparator 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库用作目录和表名之间的分隔符的字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalogSeparator()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含目录分隔符的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCatalogSeparator 方法由 java.sql.DatabaseMetaData 接口中的 getCatalogSeparator 方法指定。  
  
 将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，此方法返回句点（“.”）作为目录分隔符。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
