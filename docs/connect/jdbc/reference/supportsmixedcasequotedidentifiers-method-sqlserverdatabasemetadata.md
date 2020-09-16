---
description: supportsMixedCaseQuotedIdentifiers 方法 (SQLServerDatabaseMetaData)
title: supportsMixedCaseQuotedIdentifiers 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMixedCaseQuotedIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 76c68fc2-5af6-4b8d-baee-245716fdc5cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53eecace141e2066851130a50048a41af9eb8cf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450343"
---
# <a name="supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata"></a>supportsMixedCaseQuotedIdentifiers 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否将用双引号引起来的大小写混合的 SQL 标识符视为区分大小写，并以混合大小写方式存储它们。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsMixedCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>返回值  
 如果以大小写混合形式存储标识符，则为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsMixedCaseQuotedIdentifiers 方法是由 java.sql.DatabaseMetaData 接口中的 supportsMixedCaseQuotedIdentifiers 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
