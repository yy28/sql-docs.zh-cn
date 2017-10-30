---
title: "getIdentifierQuoteString 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
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
- SQLServerDatabaseMetaData.getIdentifierQuoteString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dea35a0-56a8-412c-8cd3-6539527ff597
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae48037425e4201124e92a02d7bd1e3107a6a73b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getidentifierquotestring-method-sqlserverdatabasemetadata"></a>getIdentifierQuoteString 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索**字符串**用于将 SQL 标识符引起。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getIdentifierQuoteString()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**包含引号的标识符。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getIdentifierQuoteString 方法指定此 getIdentifierQuoteString 方法。  
  
 使用时[!INCLUDE[msCoName](../../../includes/msconame_md.md)]JDBC 驱动程序与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，此方法返回**double**引号 ("")。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

