---
title: getServerName 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd2d58a2c47553fee1d5c8d4cf9355998078e4d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
