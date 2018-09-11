---
title: setPacketSize 方法 (SQLServerDataSource) |Microsoft Docs
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
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c99c8516c6e38400798921aeae01f2387066e228
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786053"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的当前网络数据包大小，以字节为单位指定。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parameters  
 *packetSize*  
  
 一个 int 值，此值包含网络数据包大小。  
  
## <a name="remarks"></a>Remarks  
 此属性可接受的值范围是 [-1 | 0 | 512..32767]。 如果将此属性设置为可接受范围外的值，将出现异常。  
  
 在使用 SSL（安全套接字层）加密功能连接时，应用程序可能希望设置 packetSize 属性。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将与服务器协商数据包大小。 如果加密属性设置为“true”，并且协商的数据包大小大于 Java 虚拟机 (JVM) 默认安全提供程序的 SSL 记录大小，驱动程序则将报错并终止连接。  
  
 此外，应用程序可能还希望在不要求 SSL 加密的情况下设置 packetSize 属性。 在此情况下，如果服务器要求客户端支持 SSL 加密，则驱动程序将查看 JVM 的默认安全提供程序的 SSL 记录大小。 如果 packetSize 属性大于 JVM 的默认安全提供程序的 SSL 记录大小，则驱动程序将报告错误并终止连接。  
  
 有关使用 SSL 的详细信息，请参阅[Using SSL Encryption](../../../connect/jdbc/using-ssl-encryption.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
