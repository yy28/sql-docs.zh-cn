---
title: "catalog.catalog_properties （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca3d5da05126d5b71bf6d714f9e8449f9f5c8335
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录的属性。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|目录属性的名称。|  
|property_value|**nvarchar(256)**|目录属性的值。|  
  
## <a name="remarks"></a>注释  
 此视图对于每个目录属性显示一行。 此视图显示的属性包括如下：  
  
|属性名称|Description|  
|-------------------|-----------------|  
|**ENCRYPTION_ALGORITHM**|用于加密敏感数据的加密算法的类型。 支持的值包括：`DES`、`TRIPLE_DES`、`TRIPLE_DES_3KEY`、`DESX`、`AES_128`、`AES_192` 和 `AES_256`。 注意：要更改此属性，目录数据库必须处于单用户模式。|  
|**MAX_PROJECT_VERSIONS**|将为单个项目保留的新项目版本的数量。 当启用了版本清理时，超出了此计数的较早版本将被删除。|  
|**OPERATION_CLEANUP_ENABLED**|当值是`TRUE`，操作详细信息和操作消息早于**RETENTION_WINDOW**从目录中删除 （天）。 当值为 `FALSE` 时，将在目录中存储所有操作详细信息和操作消息。 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作业执行清理操作。|  
|**RETENTION_WINDOW**|操作详细信息和操作消息存储在目录中的天数。 如果值为 `-1`，则保持期窗口是无限的。 注意： 如果需要任何清理，请设置**OPERATION_CLEANUP_ENABLED**到**FALSE**。|  
|**VALIDATION_TIMEOUT**|如果验证没有在该属性指定的秒数内完成，则将停止验证。|  
|**VERSION_CLEANUP_ENABLED**|当值是`TRUE`，则只**MAX_PROJECT_VERSIONS**项目版本数存储在目录和所有其他项目版本将被删除。 当值是**FALSE**，所有项目版本都存储在目录中。 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作业执行清理操作。|  
|**SERVER_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的默认日志记录级别。|  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
  

