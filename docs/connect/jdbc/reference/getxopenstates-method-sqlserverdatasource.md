---
title: getXopenStates 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f40bd51344b7e3fcdac7712f53e7308657f6d9bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814425"
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>getXopenStates 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回指示是否启用了将 SQL 状态转换为 XOPEN 兼容状态的 boolean 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>返回值  
 如果启用了将 SQL 状态转换为 XOPEN 兼容状态，则为 true。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果将 xopenStates 属性设置为 true，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 会将 SQL 状态转换为 XOPEN 兼容状态。 默认为 false，这将导致 JDBC 驱动程序生成 SQL 99 状态代码。 如果未设置 xopenStates，则 getXopenStates 方法会返回默认值 false。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
