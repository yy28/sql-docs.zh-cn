---
title: getLastUpdateCount 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3e15720ad49cd90af30235a7c7a7d92ca104c78
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733325"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个指示是否启用 lastUpdateCount 属性的 Boolean 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>返回值  
 如果启用了 lastUpdateCount，则为 true。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果将 lastUpdateCount 属性设置为 true，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将只返回由 SQL 语句传递给服务器的最后更新计数。 如果将 lastUpdateCount 属性设置为 false，则驱动程序将返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数。 如果未设置 lastUpdateCount 属性，则 getLastUpdateCount 方法将返回默认值 true。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
