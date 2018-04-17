---
title: sys.service_broker_endpoints (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9bfbe05a6cef26dc891c0b2b8069c26ec4a55e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Service Broker 端点在此目录视图中占一行。 此视图中每一行，存在不具有相同的相应行**endpoint_id**中**sys.tcp_endpoints**包含 TCP 配置元数据的视图。 TCP 是唯一允许 Service Broker 使用的协议。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**|**--**|继承中的列[sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)。|  
|**is_message_forwarding_enabled**|**bit**|端点支持消息转发。 这最初设置为**0** （禁用）。 不可为 NULL。|  
|**message_forwarding_size**|**int**|最大的 mb 数**tempdb**空间允许要用于转发的消息。 这最初设置为**10**。 不可为 NULL。|  
|**connection_auth**|**tinyint**|连接到此端点所需的连接身份验证的类型，为以下值之一：<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -协商<br /><br /> **4** -证书<br /><br /> **5** -NTLM、 CERTIFICATE<br /><br /> **6** -KERBEROS、 CERTIFICATE<br /><br /> **7** -NEGOTIATE、 CERTIFICATE<br /><br /> **8** -CERTIFICATE、 NTLM<br /><br /> **9** -CERTIFICATE、 KERBEROS<br /><br /> **10** -CERTIFICATE、 NEGOTIATE<br /><br /> 不可为 NULL。|  
|**connection_auth_desc**|**nvarchar(60)**|连接到此端点所需的连接身份验证类型的说明，可以是下列值之一：<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM、CERTIFICATE<br /><br /> KERBEROS、CERTIFICATE<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> CERTIFICATE、NEGOTIATE<br /><br /> 可以为 NULL。|  
|**certificate_id**|**int**|身份验证所用证书的 ID（如果有）。<br /><br /> 0 = 使用 Windows 身份验证。|  
|**encryption_algorithm**|**tinyint**|加密算法。 以下是使用其说明和相应 DDL 选项可能的值。<br /><br /> **0** ： 无。 相应 DDL 选项： 已禁用。<br /><br /> **1** : RC4。 相应 DDL 选项: {所需&#124;所需的算法 RC4}。<br /><br /> **2** : AES。 相应 DDL 选项： 所需算法 AES。<br /><br /> **3** ： 无、 RC4。 相应 DDL 选项: {支持&#124;支持算法 RC4}。<br /><br /> **4** ： 无、 AES。 相应 DDL 选项： 支持算法 AES。<br /><br /> **5** : RC4、 AES。 相应 DDL 选项： 所需算法 RC4 AES。<br /><br /> **6** : AES、 RC4。 相应 DDL 选项： 所需算法 AES RC4。<br /><br /> **7** ： 无、 RC4、 AES。 相应 DDL 选项： 支持算法 RC4 AES。<br /><br /> **8** ： 无、 AES RC4。 相应 DDL 选项： 支持算法 AES RC4。<br /><br /> 不可为 NULL。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|加密算法说明。 下面列出了可能的值和其相应的 DDL 选项：<br /><br /> NONE： 禁用<br /><br /> RC4: {所需&#124;所需算法 RC4}<br /><br /> AES： 所需算法 AES<br /><br /> 无、 RC4: {支持&#124;支持算法 RC4}<br /><br /> 无、 AES： 受支持的算法 AES<br /><br /> RC4、 AES： 所需算法 RC4 AES<br /><br /> AES、 RC4： 所需的算法 AES RC4<br /><br /> 无、 RC4、 AES： 支持算法 RC4 AES<br /><br /> 无、 AES RC4： 支持算法 AES RC4<br /><br /> 可以为 NULL。|  
  
## <a name="remarks"></a>注释  
  
> [!NOTE]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更高版本中，可以在任何兼容性级别对使用 RC4 或 RC4_128 加密的材料进行解密。  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER ENDPOINT (Transact-SQL)](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [创建终结点 & #40;Transact SQL & #41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
