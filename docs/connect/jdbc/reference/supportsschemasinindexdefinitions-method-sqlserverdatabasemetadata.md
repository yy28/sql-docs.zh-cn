---
description: supportsSchemasInIndexDefinitions 方法 (SQLServerDatabaseMetaData)
title: supportsSchemasInIndexDefinitions 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSchemasInIndexDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 55ce9e4f-6e3f-482a-93a5-b9ae1b91d7a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c598ef1193345ef49ae302d2ad2740b655662dc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450221"
---
# <a name="supportsschemasinindexdefinitions-method-sqlserverdatabasemetadata"></a>supportsSchemasInIndexDefinitions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索架构名称能否用于索引定义语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsSchemasInIndexDefinitions()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsSchemasInIndexDefinitions 方法是由 java.sql.DatabaseMetaData 接口中的 supportsSchemasInIndexDefinitions 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
