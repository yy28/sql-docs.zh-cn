---
title: getFetchDirection 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3944990d8b6f551ba70545e5cacf42179e7b68ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617085"
---
# <a name="getfetchdirection-method-sqlserverstatement"></a>getFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索从数据库表中提取行的方向，这是通过此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象生成的结果集的默认方向。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前未实现此方法。 因此，它将始终返回 FETCH_UNKNOWN。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>返回值  
 指示由 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md) 方法指定的提取方向的 int 值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getFetchDirection 方法由 java.sql.Statement 接口中的 getFetchDirection 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
