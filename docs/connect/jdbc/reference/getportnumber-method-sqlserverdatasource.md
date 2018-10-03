---
title: getPortNumber 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30b2387b4685440de737ad9e6be7d351ded86506
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736627"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的当前端口号。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值包含当前端口号。  
  
## <a name="remarks"></a>Remarks  
 此端口号是打开与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的套接字连接时使用的 TCP/IP 端口号。 如果未设置 portNumber 属性，getPortNumber 方法将返回默认值 1433。  
  
> [!NOTE]  
>  [SetPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)方法不执行任何范围检查传入的端口值。 可以传递无效的如 99999，而不引发错误号。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
