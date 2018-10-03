---
title: sys.service_broker_endpoints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f93ac0b4a11e10d3db952fd850f4c83668a97d3b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736045"
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Service Broker 端点在此目录视图中占一行。 此视图中的每一行，对于没有对应的行具有相同**endpoint_id**中**sys.tcp_endpoints**包含 TCP 配置元数据的视图。 TCP 是唯一允许 Service Broker 使用的协议。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**|**--**|继承中的列[sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)。|  
|**is_message_forwarding_enabled**|**bit**|端点支持消息转发。 此值最初设置为**0** （禁用）。 不可为 NULL。|  
|**message_forwarding_size**|**int**|兆字节的最大数目**tempdb**允许使用空格以用于要转发的消息。 此值最初设置为**10**。 不可为 NULL。|  
|**connection_auth**|**tinyint**|连接到此端点所需的连接身份验证的类型，为以下值之一：<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -协商<br /><br /> **4** -证书<br /><br /> **5** -NTLM、 CERTIFICATE<br /><br /> **6** -KERBEROS、 CERTIFICATE<br /><br /> **7** -NEGOTIATE、 CERTIFICATE<br /><br /> **8** -CERTIFICATE、 NTLM<br /><br /> **9** -CERTIFICATE、 KERBEROS<br /><br /> **10** -CERTIFICATE、 NEGOTIATE<br /><br /> 不可为 NULL。|  
|**connection_auth_desc**|**nvarchar(60)**|连接到此端点所需的连接身份验证类型的说明，可以是下列值之一：<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM、CERTIFICATE<br /><br /> KERBEROS、CERTIFICATE<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> CERTIFICATE、NEGOTIATE<br /><br /> 可以为 NULL。|  
|**certificate_id**|**int**|身份验证所用证书的 ID（如果有）。<br /><br /> 0 = 使用 Windows 身份验证。|  
|**encryption_algorithm**|**tinyint**|加密算法。 以下是带有其说明和相应的 DDL 选项的可能值。<br /><br /> **0** ： 无。 相应的 DDL 选项： 已禁用。<br /><br /> **1** : RC4。 相应的 DDL 选项: {所需&#124;所需的算法 RC4}。<br /><br /> **2** : AES。 相应的 DDL 选项： 所需算法 AES。<br /><br /> **3** : NONE、 RC4。 相应的 DDL 选项: {支持&#124;支持算法 RC4}。<br /><br /> **4** : NONE、 AES。 相应的 DDL 选项： 支持算法 AES。<br /><br /> **5** : RC4、 AES。 相应的 DDL 选项： 所需算法 RC4 AES。<br /><br /> **6** : AES、 RC4。 相应的 DDL 选项： 所需算法 AES RC4。<br /><br /> **7** : NONE、 RC4 AES。 相应的 DDL 选项： 支持算法 RC4 AES。<br /><br /> **8** : NONE、 AES RC4。 相应的 DDL 选项： 支持算法 AES RC4。<br /><br /> 不可为 NULL。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|加密算法说明。 下面列出了可能的值及其相应的 DDL 选项：<br /><br /> NONE： 已禁用<br /><br /> RC4: {所需&#124;所需算法 RC4}<br /><br /> AES： 所需算法 AES<br /><br /> 无、 RC4: {支持&#124;支持算法 RC4}<br /><br /> 无、 AES： 受支持的算法 AES<br /><br /> RC4、 AES： 所需算法 RC4 AES<br /><br /> AES、 RC4： 所需的算法 AES RC4<br /><br /> 无、 RC4 AES： 支持算法 RC4 AES<br /><br /> 无、 AES RC4： 支持算法 AES RC4<br /><br /> 可以为 NULL。|  
  
## <a name="remarks"></a>备注  
  
> [!NOTE]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更高版本中，可以在任何兼容性级别对使用 RC4 或 RC4_128 加密的材料进行解密。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [ALTER ENDPOINT (Transact-SQL)](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT (Transact-SQL)](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
