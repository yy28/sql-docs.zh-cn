---
title: getLastUpdateCount 方法 (SQLServerDataSource) |Microsoft 文档
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
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a22f963d409657b645ad04b50c260fc1576b980
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**布尔**值，该值指示是否启用了 lastUpdateCount 属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果启用 lastUpdateCount。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 lastUpdateCount 属性设置为**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将返回只有的最后一个 SQL 语句中的更新计数传递到服务器。 如果 lastUpdateCount 属性设置为**false**，驱动程序将返回所有更新包括那些由任何可能都激发的触发器的计数。 如果未设置 lastUpdateCount 属性，getLastUpdateCount 方法将返回的默认值**true**。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
