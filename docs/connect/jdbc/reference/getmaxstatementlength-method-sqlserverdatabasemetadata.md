---
title: getMaxStatementLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxStatementLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f45fcf45-b9e7-4d14-a90a-ebc542ac7755
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2b4c24addcc7287aa9a291f16f0e5d469ed87c1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906564"
---
# <a name="getmaxstatementlength-method-sqlserverdatabasemetadata"></a>getMaxStatementLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在 SQL 语句中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxStatementLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getMaxStatementLength 方法是由 java.sql.DatabaseMetaData 接口中的 getMaxStatementLength 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
