---
title: "setLastUpdateCount 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.setLastUpdateCount
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dea575ca8c0baf6f4bb017dc50cebc26448f0397
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>setLastUpdateCount 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  集**布尔**值，该值指示是否启用了 lastUpdateCount 属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>Parameters  
 *lastUpdateCount*  
  
 **true**如果启用 lastUpdateCount。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 lastUpdateCount 属性设置为**true**，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将返回只有的最后一个更新计数从 SQL 语句中的传递到服务器。 如果 lastUpdateCount 属性设置为**false**，驱动程序将返回所有更新包括那些由任何可能都激发的触发器的计数。 如果未设置 lastUpdateCount 属性， [getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)方法返回的默认值**true**。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
