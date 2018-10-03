---
title: getEncrypt 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 328bf9921bc4d70ef77862edd1476e2f8f629720
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637095"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个布尔值，此值指示是否启用了 encrypt 属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>返回值  
 如果启用了加密，则为“true”。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果 encrypt 属性设置为“ture”，则在服务器已安装有证书的情况下，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将确保 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对在客户端与服务器之间发送的所有数据使用 SSL 加密。  
  
 如果未指定 encrypt 属性或此属性设置为“false”，驱动程序将不会强制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持 SSL 加密。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例未配置为强制使用 SSL 加密，则将在不进行任何加密的情况下建立连接。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例已配置为强制使用 SSL 加密，当在已正确配置的 Java 虚拟机 (JVM) 上运行时，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将自动启用 SSL 加密，否则连接将终止并且驱动程序将报错。 如果未设置加密属性，[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) 方法则将返回默认值“false”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
