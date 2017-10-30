---
title: "catalog.delete_customized_logging_level |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0aec1e34-f30b-4e5f-bba1-c26665cf2da6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a2c53009bfbd2f0876d4cf0a01cf8fa2b5bc738e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeletecustomizedlogginglevel"></a>catalog.delete_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  删除现有的自定义日志记录级别。 有关自定义日志记录级别的详细信息，请参阅[Integration Services &#40;SSIS &#41;日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>语法  
  
```sql  
delete_customized_logging_level [ @level_name = ] level_name  
  
```  
  
## <a name="arguments"></a>参数  
 [ @level_name =] *level_name*  
 现有的名称自定义要删除的日志记录级别。  
  
 *Level_name*是**nvarchar （128)**。  
  
## <a name="remarks"></a>注释  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   **ssis_admin** 数据库角色中的成员资格  
  
-   **sysadmin** 服务器角色中的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   用户没有所需的权限。  
  
  

