---
title: sysdac_history_internal (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40696085bc8eb9980d1150feade91a9edd627be0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471136"
---
# <a name="data-tier-application-tables---sysdachistoryinternal"></a>数据层应用程序表 - sysdac_history_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含为管理数据层应用程序 (DAC) 而执行的操作的相关信息。 此表存储中**dbo**的架构**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|操作的标识符|  
|**sequence_id**|**int**|标识某一操作内的步骤。|  
|**instance_id**|**uniqueidentifier**|DAC 实例的标识符。 在将此列上联接**instance_id**中的列[dbo.sysdac_instances &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)。|  
|**action_type**|**tinyint**|操作类型的标识符：<br /><br /> **0** = 部署<br /><br /> **1** = 创建<br /><br /> **2** = 重命名<br /><br /> **3** = 分离<br /><br /> **4** = 删除|  
|**action_type_name**|**varchar(19)**|操作类型的名称：<br /><br /> **deploy**<br /><br /> **create**<br /><br /> **rename**<br /><br /> **detach**<br /><br /> **delete**|  
|**dac_object_type**|**tinyint**|受操作影响的对象类型的标识符：<br /><br /> **0** = dacpac<br /><br /> **1** = 登录名<br /><br /> **2** = 数据库|  
|**dac_object_type_name**|**varchar(8)**|受操作影响的对象类型的名称：<br /><br /> **dacpac** = DAC 实例<br /><br /> **login**<br /><br /> **database**|  
|**action_status**|**tinyint**|标识当前操作状态的代码：<br /><br /> **0** = 挂起<br /><br /> **1** = 成功<br /><br /> **2** = 失败|  
|**action_status_name**|**varchar(11)**|操作的当前状态：<br /><br /> **pending**<br /><br /> **success**<br /><br /> **fail**|  
|**必需**|**bit**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]在回滚 DAC 操作时使用。|  
|**dac_object_name_pretran**|**sysname**|在提交包含操作的事务前对象的名称。 仅用于数据库和登录名。|  
|**dac_object_name_posttran**|**sysname**|在提交包含操作的事务后对象的名称。 仅用于数据库和登录名。|  
|**sqlscript**|**nvarchar(max)**|对数据库或登录名实现操作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。|  
|**payload**|**varbinary(max)**|在二进制编码字符串中保存的 DAC 包定义。|  
|**注释**|**varchar(max)**|记录接受了 DAC 升级中的潜在数据损失的用户的登录名。|  
|**error_string**|**nvarchar(max)**|在操作遇到错误时生成的错误消息。|  
|**created_by**|**sysname**|启动了创建此条目的操作的登录名。|  
|**date_created**|**datetime**|该条目的创建日期和时间。|  
|**date_modified**|**datetime**|最后修改该条目的日期和时间。|  
  
## <a name="remarks"></a>备注  
 DAC 管理操作（例如部署或删除 DAC）会产生多个步骤。 为每个操作都分配一个操作标识符。 每个步骤都分配一个序列号和中的某一行**sysdac_history_internal**，其中记录的步骤的状态。 在该操作步骤开始时创建每一行，并且根据需要进行更新以便反映该操作的状态。 例如，无法分配一个部署 DAC 操作**action_id** 12 并获取四行中**sysdac_history_internal**:  
  
|||||  
|-|-|-|-|  
|**action_id**|**sequence_id**|**action_type_name**|**dac_object_type_name**|  
|12|0|创建|dacpac|  
|12|1|创建|login|  
|12|2|创建|“数据库”|  
|12|3|重命名|“数据库”|  
  
 DAC 操作，例如删除，并删除中的行**sysdac_history_internal**。 使用以下查询可以手动删除在[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例上不再部署的 DAC 行：  
  
```sql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 为处于活动状态的 DAC 删除行并不影响 DAC 操作；唯一影响是您将不能报告 DAC 的完整历史记录。  
  
> [!NOTE]  
>  目前，没有用于删除机制**sysdac_history_internal**行的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
## <a name="permissions"></a>权限  
 要求具有 sysadmin 固定服务器角色的成员身份。 对此视图的只读访问可供有权连接到 master 数据库的所有用户。  
  
## <a name="see-also"></a>请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 [sysdac_instances_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
