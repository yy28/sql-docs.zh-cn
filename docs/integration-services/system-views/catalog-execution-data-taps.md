---
title: "catalog.execution_data_taps |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bc949b9b6111c65d6faa43a118efd03068630fe0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutiondatataps"></a>catalog.execution_data_taps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示在执行中定义的每个数据分流点的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|数据分流点的唯一标识符 (ID)。|  
|execution_id|**bigint**|执行实例的唯一标识符 (ID)。|  
|package_path|**nvarchar(max)**|分流数据的数据流任务的包路径。|  
|dataflow_path_id_string|**nvarchar(4000)**|数据流路径的标识字符串。|  
|dataflow_task_guid|**uniqueidentifier**|数据流任务的唯一 ID。|  
|max_rows|**int**|要捕获的行数。 如果未指定此值，则将捕获所有行。|  
|filename|**nvarchar(4000)**|数据转储文件的名称。 有关详细信息，请参阅 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。|  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
## <a name="see-also"></a>另请参阅  
 [生成包执行的转储文件](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
