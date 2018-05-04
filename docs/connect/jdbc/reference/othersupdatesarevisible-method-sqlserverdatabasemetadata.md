---
title: othersUpdatesAreVisible 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.othersUpdatesAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3615c01f-ae0b-42a7-92b5-e8770d841c45
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38c52f7f0297c6d565abcf4f7bf14caa884dc58a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="othersupdatesarevisible-method-sqlserverdatabasemetadata"></a>othersUpdatesAreVisible 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索人所做的更新是否可见。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean othersUpdatesAreVisible(int type)  
```  
  
#### <a name="parameters"></a>Parameters  
 *类型*  
  
 **Int** ，该值指示结果集类型，如 java.sql.ResultSet 或 SQLServerResultSet 中定义可以是以下值之一：  
  
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
 **true**如果更新是可见。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 othersUpdatesAreVisible 方法指定此 othersUpdatesAreVisible 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
