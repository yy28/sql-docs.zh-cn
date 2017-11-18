---
title: "setPacketSize 方法 (SQLServerDataSource) |Microsoft 文档"
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
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9684140ed084cc7a096675935ceec81209f8fa66
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于与进行通信的当前网络数据包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以字节为单位指定。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据包大小*  
  
 **Int**值，该值包含的网络数据包大小。  
  
## <a name="remarks"></a>注释  
 此属性可接受的值范围是 [-1 | 0 | 512..32767]。 如果将此属性设置为可接受范围外的值，将出现异常。  
  
 在使用 SSL（安全套接字层）加密功能连接时，应用程序可能希望设置 packetSize 属性。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]协商与服务器的数据包大小。 如果加密属性设置为"**true**"和协商的数据包大小大于 Java 虚拟机 (JVM) 的默认安全提供程序 SSL 记录大小，该驱动程序将引发错误并终止连接。  
  
 此外，应用程序可能还希望在不要求 SSL 加密的情况下设置 packetSize 属性。 在此情况下，如果服务器要求客户端支持 SSL 加密，则驱动程序将查看 JVM 的默认安全提供程序的 SSL 记录大小。 如果 packetSize 属性大于 JVM 的默认安全提供程序的 SSL 记录大小，则驱动程序将报告错误并终止连接。  
  
 有关使用 SSL 的详细信息，请参阅[使用 SSL 加密](../../../connect/jdbc/using-ssl-encryption.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

