---
title: setIntegratedSecurity 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7d922c2c2fcfadb6b7807b8d2845f8d3e6c5188c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780445"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置一个布尔值，此值指示是否启用了 integratedSecurity 属性  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>Parameters  
 *enable*  
  
 如果启用了 integratedSecurity，则为“true”  。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 设置为“true”表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将使用 Windows 凭据来对应用程序用户进行身份验证  。 如果为“true”，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 则将搜索本地计算机凭据缓存，以寻找在登录计算机或网络时已提供的凭据  。 如果为“false”，则必须提供用户名和密码  。  
  
> [!NOTE]  
>  只有 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows 操作系统才支持此属性。  
  
 有关使用集成身份验证的详细信息，请参阅[创建连接 URL](../../../connect/jdbc/building-the-connection-url.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
