---
title: getXopenStates 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 060b148d8cb0b8139b9ed5cd45fa698852cc1ae5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>getXopenStates 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**布尔**值，该值指示是否启用将 SQL 状态转换为 XOPEN 符合状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果启用了将 SQL 状态转换为 XOPEN 符合状态。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 xopenStates 属性设置为**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]会将 SQL 状态转换到 XOPEN 符合状态。 默认值是**false**，这将导致产生 JDBC 驱动程序为生成 SQL 99 状态代码。 如果未设置 xopenStates，getXopenStates 方法将返回的默认值**false**。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
