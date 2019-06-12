---
title: supportsCatalogsInDataManipulation 方法 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 03e938e89241c95af88a35b616791318a1b4c979
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766508"
---
# <a name="supportscatalogsindatamanipulation-method-sqlserverdatabasemetadata"></a>supportsCatalogsInDataManipulation 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索目录名称能否用于数据操作语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsCatalogsInDataManipulation()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果受支持。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 supportsCatalogInDataManipulation 方法由 java.sql.DatabaseMetaData 接口中的 supportsCatalogInDataManipulation 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
