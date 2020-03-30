---
title: getMaxColumnsInTable 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInTable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dbcad2e1-7508-49ff-9f6d-db11200d87b6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b9499dd3c146aa383f98d7ef67bcf036dd3430b8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982182"
---
# <a name="getmaxcolumnsintable-method-sqlserverdatabasemetadata"></a>getMaxColumnsInTable 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在表中允许的最大列数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxColumnsInTable()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大列数的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getMaxColumnsInTable 方法是由 java.sql.DatabaseMetaData 接口中的 getMaxColumnsInTable 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
