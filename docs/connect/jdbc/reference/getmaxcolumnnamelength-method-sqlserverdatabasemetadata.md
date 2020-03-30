---
title: getMaxColumnNameLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 67fb5407-55b9-48b6-87f3-112700f304ba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab90493a897d5b9561f3e1f4f58413a5de8e8b9e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982308"
---
# <a name="getmaxcolumnnamelength-method-sqlserverdatabasemetadata"></a>getMaxColumnNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在列名中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxColumnNameLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getMaxColumnNameLength 方法是由 java.sql.DatabaseMetaData 接口中的 getMaxColumnNameLength 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
