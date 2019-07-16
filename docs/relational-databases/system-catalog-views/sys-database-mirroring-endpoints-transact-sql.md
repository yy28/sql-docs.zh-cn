---
title: sys.database_mirroring_endpoints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bcbe9d23bab18e47b69f82812f604a94d4c5ce9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022764"
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据库镜像端点对应一行。  
  
> [!NOTE]  
>  数据库镜像终结点支持的两个会话之间数据库镜像伙伴和见证服务器和 Alwayson 可用性组的主副本和及其辅助副本之间的会话。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**|-|继承中的列**sys.endpoints** (有关详细信息，请参阅[sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md))。|  
|**角色**|**tinyint**|镜像角色，为以下值之一：<br /><br /> **0** = 无<br /><br /> **1** = partner<br /><br /> **2** = 见证服务器<br /><br /> **3** = all<br /><br /> 注意:此值是仅针对数据库镜像相关。|  
|**role_desc**|**nvarchar(60)**|镜像角色的说明，为以下值之一：<br /><br /> **NONE**<br /><br /> **合作伙伴**<br /><br /> **WITNESS**<br /><br /> **ALL**<br /><br /> 注意:此值是仅针对数据库镜像相关。|  
|**is_encryption_enabled**|**bit**|**1**表示启用加密。<br /><br /> **0**表示禁用加密。|  
|**connection_auth**|**tinyint**|连接到此端点所需的连接身份验证的类型，为以下值之一：<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -协商<br /><br /> **4** -证书<br /><br /> **5** -NTLM、 CERTIFICATE<br /><br /> **6** -KERBEROS、 CERTIFICATE<br /><br /> **7** -NEGOTIATE、 CERTIFICATE<br /><br /> **8** -CERTIFICATE、 NTLM<br /><br /> **9** -CERTIFICATE、 KERBEROS<br /><br /> **10** -CERTIFICATE、 NEGOTIATE|  
|**connection_auth_desc**|**Nvarchar (60)**|连接到此端点所需的身份验证类型的说明，为以下值之一：<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM、CERTIFICATE<br /><br /> KERBEROS、CERTIFICATE<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> CERTIFICATE、NEGOTIATE|  
|**certificate_id**|**int**|身份验证所用证书的 ID（如果有）。<br /><br /> 0 = 使用 Windows 身份验证。|  
|**encryption_algorithm**|**tinyint**|加密算法，为以下值之一：<br /><br /> **0** -无<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -无、 RC4<br /><br /> **4** -无、 AES<br /><br /> **5** -RC4、 AES<br /><br /> **6** -AES、 RC4<br /><br /> **7** -无、 RC4 AES<br /><br /> **8** -无、 AES RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|加密算法的说明，为以下值之一：<br /><br /> 无<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>备注  
  
> [!NOTE]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本，可以对使用 RC4 或 RC4_128 加密的材料解密在任何兼容性级别中。  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [指定终结点 URL 添加或修改可用性副本时&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas (Transact-SQL)](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.database_mirroring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses (Transact-SQL)](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [数据库镜像终结点 (SQL Server)](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
