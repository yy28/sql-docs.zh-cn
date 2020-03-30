---
title: supportsLimitedOuterJoins 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsLimitedOuterJoins
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 06225a1a-a58d-4bff-b2ef-be303f051644
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8e1b235a8c779c652a8678802bbb91a1de83f38
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969301"
---
# <a name="supportslimitedouterjoins-method-sqlserverdatabasemetadata"></a>supportsLimitedOuterJoins 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否可为外部联接提供有限支持。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsLimitedOuterJoins()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsLimitedOuterJoins 方法是由 java.sql.DatabaseMetaData 接口中的 supportsLimitedOuterJoins 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
