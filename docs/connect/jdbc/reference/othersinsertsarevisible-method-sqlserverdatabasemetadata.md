---
description: othersInsertsAreVisible 方法 (SQLServerDatabaseMetaData)
title: othersInsertsAreVisible 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.othersInsertsAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa32f059-bb59-47f8-bac1-292f314df730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: addf9a610270a7a2b3c6dae10c0e33dba1380552
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433109"
---
# <a name="othersinsertsarevisible-method-sqlserverdatabasemetadata"></a>othersInsertsAreVisible 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索其他人执行的插入操作是否可见。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean othersInsertsAreVisible(int type)  
```  
  
#### <a name="parameters"></a>参数  
 type  
  
 指示结果集类型的 int，它可以为 java.sql.ResultSet 或 SQLServerResultSet 中定义的以下值之一****：  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet 类型  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet 类型  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>返回值  
 如果插入操作可见，则为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 othersInsertsAreVisible 方法是由 java.sql.DatabaseMetaData 接口中的 othersInsertsAreVisible 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
