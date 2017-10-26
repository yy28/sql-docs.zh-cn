---
title: "setXopenStates 方法 (SQLServerDataSource) |Microsoft 文档"
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
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 857d9f914e10365746381ee4335f35f19d4beedd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  集**布尔**值，该值指示是否启用将 SQL 状态转换为 XOPEN 符合状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parameters  
 *xopenStates*  
  
 **true**如果启用了将 SQL 状态转换为 XOPEN 符合状态。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 xopenStates 属性设置为**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]会将 SQL 状态转换到 XOPEN 符合状态。 默认值是**false**，这将导致产生 JDBC 驱动程序为生成 SQL 99 状态代码。 如果未设置 xopenStates， [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)方法返回的默认值**false**。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

