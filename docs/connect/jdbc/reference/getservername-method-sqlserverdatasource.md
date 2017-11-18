---
title: "getServerName 方法 (SQLServerDataSource) |Microsoft 文档"
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
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f7c77c52a62465eea584e3fa695810a65ffc202
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getservername-method-sqlserverdatasource"></a>getServerName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回的名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**如果未不设置任何值包含的服务器名称或为 null。  
  
## <a name="remarks"></a>注释  
 服务器名称是正在运行的目标计算机的主机名[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 如果未设置 getServerName 属性，getServerName 返回默认值为 null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

