---
title: getPacketSize 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7790bc9eabb5127e36faddc02bb477c91ba72ac6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838975"
---
# <a name="getpacketsize-method-sqlserverdatasource"></a>getPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的当前网络数据包大小，以字节为单位指定。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值包含当前的网络数据包大小。  
  
## <a name="remarks"></a>Remarks  
 如果未设置 packetSize 属性，getPacketSize 方法则将返回默认值 8000。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
