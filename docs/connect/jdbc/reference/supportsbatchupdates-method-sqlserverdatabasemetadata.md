---
title: supportsBatchUpdates 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsBatchUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 47b7b0da-e467-465a-aa19-bc702efcfaa0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f7ffdc84d40f68b1f1697357a892fb2d136be2e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766515"
---
# <a name="supportsbatchupdates-method-sqlserverdatabasemetadata"></a>supportsBatchUpdates 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持批更新。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsBatchUpdates()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果受支持。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 supportsBatchUpdates 方法由 java.sql.DatabaseMetaData 接口中的 supportsBatchUpdates 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
