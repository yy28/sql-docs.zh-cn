---
title: setLoginTimeout 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b655449b2b15e7fbf1f31f7045bc5f0051951a2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681115"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象在尝试建立连接时将等待的秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parameters  
 *loginTimeout*  
  
 一个表示要等待的秒数的 int 值。 零表示该超时为默认系统超时，默认情况下指定为 15 秒。  
  
## <a name="remarks"></a>Remarks  
 此 setLoginTimeout 方法由 javax.sql.DataSource 接口中的 setLoginTimeout 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
