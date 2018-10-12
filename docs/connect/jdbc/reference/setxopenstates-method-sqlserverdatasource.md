---
title: setXopenStates 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65fde7feacb27f8c3b7fb2d809de4f75bc7e899c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695865"
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置指示是否启用了将 SQL 状态转换为 XOPEN 兼容状态的 Boolean 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parameters  
 *xopenStates*  
  
 如果启用了将 SQL 状态转换为 XOPEN 兼容状态，则为 true。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果将 xopenStates 属性设置为 true，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 会将 SQL 状态转换为 XOPEN 兼容状态。 默认为 false，这将导致 JDBC 驱动程序生成 SQL 99 状态代码。 如果未设置 xopenStates，则 [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) 方法会返回默认值 false。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
