---
title: "getFetchDirection 方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ae039ccdc76cdc6117f502971feafe683f58b0d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getfetchdirection-method-sqlserverstatement"></a>getFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索从数据库表提取行是从生成的结果集的默认方向[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。  
  
> [!NOTE]  
>  此方法当前未实现通过[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 因此，它将始终返回 FETCH_UNKNOWN。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示由指定的提取方向[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)方法。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 getFetchDirection 方法指定此 getFetchDirection 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
