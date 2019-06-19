---
title: sysssispackages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3e25d69b4ba7887d20ef86ff771a3f10864ddbd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489799"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  保存到的每个包中对应一行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此表存储中**msdb**数据库。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|包的唯一标识符。|  
|**id**|**uniqueidentifier**|包的 GUID。|  
|**description**|**nvarchar**|包的可选说明。|  
|**createdate**|**datetime**|包的创建日期。|  
|**folderid**|**uniqueidentifier**|逻辑文件夹的 GUID，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在该文件夹中列出包。|  
|**ownersid**|**varbinary**|创建了包的用户的唯一安全标识符。|  
|**packagedata**|**image**|包。|  
|**packageformat**|**int**|包的保存格式：<br /><br /> 值为 2 表示包保存在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]格式。<br /><br /> 值为 3 指示的格式保存包[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]或更高版本。|  
|**packagetype**|**int**|创建了包的客户端。 可能的值如下：<br /><br /> 0（默认值）<br /><br /> 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导)<br /><br /> 3 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]复制)<br /><br /> 5 ([!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器)<br /><br /> 6（维护计划设计器或向导）<br /><br /> <br /><br /> 请注意，此列中的值对应于<xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>枚举。|  
|**vermajor**|**int**|包的最新主版本。|  
|**verminor**|**int**|包的最新次版本。|  
|**verbuild**|**int**|包的最新版本。|  
|**vercomments**|**nvarchar**|包版本的注释。|  
|**verid**|**uniqueidentifier**|包版本 GUID。|  
|**isencrypted**|**bit**|指示包是否加密的布尔值。|  
|**readrolesid**|**varbinary**|可以加载包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
|**writerolesid**|**varbinary**|可以保存包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 包](../../integration-services/integration-services-ssis-packages.md)  
  
  
