---
title: "catalog.set_customized_logging_level_value |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 75ef405fe4550e81ec2d5178a1d3242d405755af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedlogginglevelvalue"></a>catalog.set_customized_logging_level_value
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  更改统计信息或事件所记录的一个现有的自定义日志记录级别。 有关自定义日志记录级别的详细信息，请参阅[Integration Services &#40;SSIS &#41;日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>参数  
 [ @level_name =] *level_name*  
 现有的名称的自定义日志记录级别。  
  
 *Level_name*是**nvarchar （128)**。  
  
 [ @property_name =] *property_name*  
 要更改的属性名称。 有效值为**配置文件**和**事件**。  
  
 *Property_name*是**nvarchar （128)**。  
  
 [ @property_value =] *property_value*  
 指定的指定属性的新值的自定义日志记录级别。  
  
 有关为配置文件和事件的有效值的列表，请参阅[catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)。  
  
 *Property_value*是**bigint**。  
  
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
  
  
