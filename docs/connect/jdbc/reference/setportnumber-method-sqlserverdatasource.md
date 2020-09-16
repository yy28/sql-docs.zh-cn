---
description: setPortNumber 方法 (SQLServerDataSource)
title: setPortNumber 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbf1cccfab3cef60193cc9b45921c203821cbfca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458479"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>setPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的端口号。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>参数  
 *portNumber*  
  
 一个 int 值，此值包含端口号****。  
  
## <a name="remarks"></a>注解  
 此端口号是打开与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的套接字连接时使用的 TCP/IP 端口号。 如果未设置 portNumber 属性，[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 方法将返回默认值 1433。  
  
> [!NOTE]  
>  setPortNumber 方法不对传入的端口值进行任何范围检查。 可以传递无效的端口号（如 99999），而不会触发错误。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
