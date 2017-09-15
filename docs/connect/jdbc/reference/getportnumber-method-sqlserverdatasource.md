---
title: "getPortNumber 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2cf2e36d551a3b9e2e6e990c4945708043277e6a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于与进行通信的当前端口号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>返回值  
 **Int**值，该值包含当前端口号。  
  
## <a name="remarks"></a>注释  
 端口号是打开到套接字连接时使用的 TCP/IP 端口号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 如果未设置 portNumber 属性，getPortNumber 方法将返回默认值 1433。  
  
> [!NOTE]  
>  [SetPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)方法不执行任何检查传入的端口值的范围。 你可以将传递不是有效的如 99999，而不会触发错误的侵权行为引起数字。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
