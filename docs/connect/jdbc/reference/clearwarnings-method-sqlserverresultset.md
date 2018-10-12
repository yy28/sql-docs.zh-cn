---
title: clearWarnings 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.clearWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f55af4b6-ae5c-41c9-8aa3-8313773f5443
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2cdba3c27c440fbe69e499634a755586aac2058
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733705"
---
# <a name="clearwarnings-method-sqlserverresultset"></a>clearWarnings 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  清除此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象上所报告的所有警告。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前未实现此方法。 如果调用，它将始终返回 null。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void clearWarnings()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 clearWarnings 方法由 java.sql.ResultSet 接口中的 clearWarnings 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
