---
title: nullsAreSortedHigh 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedHigh
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ff97d37-befc-47b1-8092-505917216a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46f8df147dda25a7b3d8dac33121a25622962950
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976635"
---
# <a name="nullsaresortedhigh-method-sqlserverdatabasemetadata"></a>nullsAreSortedHigh 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 NULL 值是否在排序中位置较高。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean nullsAreSortedHigh()  
```  
  
## <a name="return-value"></a>返回值  
 如果该值在排序中位置较高，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 nullsAreSortedHigh 方法是由 java.sql.DatabaseMetaData 接口中的 nullsAreSortedHigh 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
