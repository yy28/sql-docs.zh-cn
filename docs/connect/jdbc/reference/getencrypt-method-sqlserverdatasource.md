---
title: "getEncrypt 方法 (SQLServerDataSource) |Microsoft 文档"
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
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8edaf27e2c08b1738d8dedc3e059c0fecb5043b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**布尔**值，该值指示是否启用了加密属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果加密已启用。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果加密属性设置为**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]确保[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]如果服务器已安装的证书客户端和服务器之间发送的所有数据使用 SSL 加密。  
  
 如果未指定或设置为加密属性**false**，驱动程序将不会强制[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]若要支持 SSL 加密。 如果[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例未配置为强制 SSL 加密，而无需任何加密建立的连接。 如果[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例配置为强制 SSL 加密，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]时会自动启用 SSL 加密上正确运行配置 Java 虚拟机 (JVM)，否则的连接被终止，并将引发该驱动程序错误。 如果未设置加密属性， [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)方法返回的默认值**false**。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

