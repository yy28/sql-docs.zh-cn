---
title: "catalog.environment_variables （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 40e31b9697c453f6a9d60dfcc8d9302dfefe0ac4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogenvironmentvariables-ssisdb-database"></a>catalog.environment_variables（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有环境的环境变量详细信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|环境变量的唯一标识符 (ID)。|  
|environment_id|**bigint**|与环境变量关联的环境的唯一 ID。|  
|name|**sysname**|环境变量的名称。|  
|description|**nvarchar(1024)**|环境变量的说明。|  
|类型|**nvarchar （128)**|环境变量的数据类型。|  
|sensitive|**bit**|当值为 `1` 时，变量是敏感的并在存储时加密。 当值为 `0` 时，变量是不敏感的并以纯文本形式存储值。|  
|值|**sql_variant**|环境变量的值。 当敏感是`0`，显示纯文本值。 当敏感是`1`、 **NULL**显示值。|  
  
## <a name="remarks"></a>注释  
 此视图对于目录中的每个环境变量显示一行。  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对相应环境的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  
