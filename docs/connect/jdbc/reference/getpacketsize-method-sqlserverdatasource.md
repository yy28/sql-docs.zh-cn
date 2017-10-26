---
title: "getPacketSize 方法 (SQLServerDataSource) |Microsoft 文档"
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
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9788a804580b88d9f65f9df8e176d883863aa1a0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getpacketsize-method-sqlserverdatasource"></a>getPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于与进行通信的当前网络数据包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以字节为单位指定。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>返回值  
 **Int**值，该值包含当前的网络数据包大小。  
  
## <a name="remarks"></a>注释  
 如果未设置数据包大小属性，getPacketSize 方法将返回默认值为 8000。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

