---
title: storesLowerCaseQuotedIdentifiers 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.storesLowerCaseQuotedIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3e104c9e-66d4-436b-8b5b-a00ff667c95b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58135670e18af30dd8795cc124eb43908f611e24
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969980"
---
# <a name="storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata"></a>storesLowerCaseQuotedIdentifiers 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否将用双引号引起来的大小写混合的 SQL 标识符视为不区分大小写，并以小写方式存储它们。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean storesLowerCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>返回值  
 如果以小写形式存储标识符，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 storesLowerCaseQuotedIdentifiers 方法是由 java.sql.DatabaseMetaData 接口中的 storesLowerCaseQuotedIdentifiers 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
