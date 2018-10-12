---
title: othersInsertsAreVisible 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b124003525af7f461057d3183b5ed185f54410c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690305"
---
# <a name="othersinsertsarevisible-method-sqlserverdatabasemetadata"></a>othersInsertsAreVisible 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索其他人执行的插入操作是否可见。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean othersInsertsAreVisible(int type)  
```  
  
#### <a name="parameters"></a>Parameters  
 *type*  
  
 指示结果集类型的 int，它可以为 java.sql.ResultSet 或 SQLServerResultSet 中定义的以下值之一：  
  
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
 如果插入操作可见，则为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 othersInsertsAreVisible 方法由 java.sql.DatabaseMetaData 接口中的 othersInsertsAreVisible 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
