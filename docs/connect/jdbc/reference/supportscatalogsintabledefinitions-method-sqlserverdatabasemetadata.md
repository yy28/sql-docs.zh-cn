---
description: supportsCatalogsInTableDefinitions 方法 (SQLServerDatabaseMetaData)
title: supportsCatalogsInTableDefinitions 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInTableDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e1e50ac-f3d4-416a-8a69-d8b7b4f30bf3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9552de356220f1e672a19b2ff5e77e65464ade1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431509"
---
# <a name="supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata"></a>supportsCatalogsInTableDefinitions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索目录名称能否用于表定义语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsCatalogsInTableDefinitions()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsCatalogsInTableDefinitions 方法是由 java.sql.DatabaseMetaData 接口中的 supportsCatalogsInTableDefinitions 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
