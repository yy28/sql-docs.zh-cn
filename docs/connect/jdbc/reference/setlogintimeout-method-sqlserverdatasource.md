---
title: "setLoginTimeout 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e95a0377de7fe9a901f33b5913e70399b298aba
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  集的秒数的这[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象将在尝试建立连接时等待。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parameters  
 *loginTimeout*  
  
 **Int**表示等待的秒数的值。 零表示该超时为默认系统超时，默认情况下指定为 15 秒。  
  
## <a name="remarks"></a>注释  
 由 javax.sql.DataSource 接口中的 setLoginTimeout 方法指定此 setLoginTimeout 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

