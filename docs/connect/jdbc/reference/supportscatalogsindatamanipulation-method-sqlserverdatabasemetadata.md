---
title: supportsCatalogsInDataManipulation 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInDataManipulation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee1af47a-4c04-4391-83a5-54ced80218c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bed23d0a0781de7c384e61cb09903e2ab2136268
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969733"
---
# <a name="supportscatalogsindatamanipulation-method-sqlserverdatabasemetadata"></a>supportsCatalogsInDataManipulation 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索目录名称能否用于数据操作语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsCatalogsInDataManipulation()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsCatalogInDataManipulation 方法是由 java.sql.DatabaseMetaData 接口中的 supportsCatalogInDataManipulation 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
