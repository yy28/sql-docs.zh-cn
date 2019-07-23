---
title: setUser 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 945033f96b5c8c36ea7b3d4c75aafa382a057164
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972071"
---
# <a name="setuser-method-sqlserverdatasource"></a>setUser 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于连接数据源的用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>Parameters  
 user   
  
 一个包含用户名的字符串  。  
  
## <a name="remarks"></a>Remarks  
 setUser 方法设置将用于连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的用户名。 如果未设置用户名值，[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) 方法则返回默认值 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
