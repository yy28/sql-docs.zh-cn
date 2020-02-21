---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c171e8fb78553275d6a1f5d4bcce485a470f94a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973188"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>setPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的端口号。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>parameters  
 *portNumber*  
  
 一个 int 值，此值包含端口号  。  
  
## <a name="remarks"></a>备注  
 此端口号是打开与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的套接字连接时使用的 TCP/IP 端口号。 如果未设置 portNumber 属性，[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 方法将返回默认值 1433。  
  
> [!NOTE]  
>  setPortNumber 方法不对传入的端口值进行任何范围检查。 可以传递无效的端口号（如 99999），而不会触发错误。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
