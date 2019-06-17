---
title: supportsSubqueriesInQuantifieds 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSubqueriesInQuantifieds
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6749e14c-0f8a-4f1f-8583-dd5cc79b24fe
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 471d8bec6d1491ed8e2ddabbf819abdfa68db16d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797263"
---
# <a name="supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata"></a>supportsSubqueriesInQuantifieds 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持限定表达式中的子查询。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsSubqueriesInQuantifieds()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果受支持。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 supportsSubqueriesInQuantifieds 方法由 java.sql.DatabaseMetaData 接口中的 supportsSubqueriesInQuantifieds 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
