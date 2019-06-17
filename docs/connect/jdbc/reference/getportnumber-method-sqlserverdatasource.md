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
manager: jroth
ms.openlocfilehash: b731bf5ce8272fe72167d77b96e523cd3ede1139
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771332"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的当前端口号。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值包含当前端口号  。  
  
## <a name="remarks"></a>Remarks  
 此端口号是打开与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的套接字连接时使用的 TCP/IP 端口号。 如果未设置 portNumber 属性，getPortNumber 方法将返回默认值 1433。  
  
> [!NOTE]  
>  [SetPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)方法不执行任何范围检查传入的端口值。 可以传递无效的如 99999，而不引发错误号。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
