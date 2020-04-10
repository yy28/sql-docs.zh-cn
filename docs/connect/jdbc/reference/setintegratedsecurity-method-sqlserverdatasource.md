---
title: setIntegratedSecurity 方法 (SQLServerDataSource) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3c01360160093465919625757e29602494860f2f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922251"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置一个布尔值，此值指示是否启用了 integratedSecurity 属性  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>parameters  
 *enable*  
  
 如果启用了 integratedSecurity，则为“true”  。 否则为 **false**。  
  
## <a name="remarks"></a>备注  
 设置为“true”表示  **将使用 Windows 凭据来对应用程序用户进行身份验证**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如果为“true”， **则将搜索本地计算机凭据缓存，以寻找在登录计算机或网络时已提供的凭据**[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 如果为“false”，则必须提供用户名和密码  。  
  
> [!NOTE]  
>  只有 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows 操作系统才支持此属性。  
  
 有关使用集成身份验证的详细信息，请参阅[生成连接 URL](../../../connect/jdbc/building-the-connection-url.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
