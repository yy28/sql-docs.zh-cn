---
title: 在目标服务器上设置加密选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b27dd81df572e289d182fdaa637a3af972b3d603
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63244979"
---
# <a name="set-encryption-options-on-target-servers"></a>在目标服务器上设置加密选项
  如果您无法在主服务器和某些或所有目标服务器之间的安全套接字层 (SSL) 加密通信中使用证书，但希望对它们之间的通道进行加密，则请将目标服务器配置为使用所需的安全级别。  
  
 若要为特定的主服务器/目标服务器通信通道配置所需的适当安全级别，请[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将目标服务器上的代理注册表子项**\\\HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server****>**** \<instance_name \SQLServerAgent\MsxEncryptChannelOptions （REG_DWORD）设置为以下值之一。 \< *Instance_name*> 的值为**MSSQL。**_n_。 例如， **MSSQL.1** 或 **MSSQL.3**。  
  
|值|说明|  
|-----------|-----------------|  
|**0**|在该目标服务器和主服务器之间禁用加密。 请仅在目标服务器和主服务器之间的通道已使用其他方法进行了保护时才选择此选项。|  
|**1**|仅在该目标服务器和主服务器之间启用加密，但不需要证书验证。|  
|**2**|在该目标服务器和主服务器之间启用完全 SSL 加密和证书验证。 此设置为默认设置。 除非出于特定的原因要选择其他值，否则建议不要对其进行更改。|  
  
 如果指定了 **1** 或 **2** ，则必须同时在主服务器和目标服务器上启用 SSL。 如果指定了 **2** ，则还必须在主服务器上安装相应的签名证书。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
  
