---
title: sysssispackages （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 1fa0f587fc5939135b3d88b15066de29be6d8a7c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889246"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  保存到的每个包在列中占一行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 该表存储在**msdb**数据库中。  
  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|**sysname**|包的唯一标识符。|  
|**id**|**uniqueidentifier**|包的 GUID。|  
|**2008**|**nvarchar**|包的可选说明。|  
|**createdate**|**datetime**|包的创建日期。|  
|**folderid**|**uniqueidentifier**|逻辑文件夹的 GUID，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在该文件夹中列出包。|  
|**ownersid**|**varbinary**|创建了包的用户的唯一安全标识符。|  
|**packagedata**|**图像**|包。|  
|**packageformat**|**int**|包的保存格式：<br /><br /> 值为2表示以格式保存包 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。<br /><br /> 值为3表示以 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或更高的格式保存包。|  
|**packagetype**|**int**|创建了包的客户端。 可能的值如下：<br /><br /> 0（默认值）<br /><br /> 1（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导）<br /><br /> 3（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制）<br /><br /> 5（ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器）<br /><br /> 6（维护计划设计器或向导）<br /><br /> <br /><br /> 请注意，此列中的值对应于 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType> 枚举。|  
|**vermajor**|**int**|包的最新主版本。|  
|**verminor**|**int**|包的最新次版本。|  
|**verbuild**|**int**|包的最新版本。|  
|**vercomments**|**nvarchar**|包版本的注释。|  
|**verid**|**uniqueidentifier**|包版本的 GUID。|  
|**isencrypted**|**bit**|指示包是否加密的布尔值。|  
|**readrolesid**|**varbinary**|可以加载包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
|**writerolesid**|**varbinary**|可以保存包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 包](../../integration-services/integration-services-ssis-packages.md)  
  
  
