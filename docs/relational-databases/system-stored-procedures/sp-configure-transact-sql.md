---
title: sp_configure (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fb4aeced22755ff2b8012e5eeff7c27ec2f73374
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476013"
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  显示或更改当前服务器的全局配置设置。

> [!NOTE]  
>  有关数据库级配置选项, 请参阅[ALTER DATABASE 作用域&#40;配置 transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要配置软件 NUMA, 请参阅[软 numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>参数  
`[ @configname = ] 'option_name'`配置选项的名称。 *option_name* 的数据类型为 **varchar(35)** ，默认值为 NULL。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]能够识别构成配置名称的任何唯一字符串。 如果未指定该参数，则返回选项的完整列表。  
  
 有关可用配置选项及其设置的信息, 请参阅[服务器配置选项&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
`[ @configvalue = ] 'value'`新的配置设置。 *value* 的数据类型为 **int**，默认值为 NULL。 最大值取决于各个选项。  
  
 若要查看每个选项的最大值, 请参阅**sys.databases**目录视图的**最大**值列。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 在不带参数的情况下执行时, **sp_configure**会返回五列的结果集, 并按字母顺序升序排列选项, 如下表所示。  
  
 **Config_value**和**run_value**的值不是自动等效的。 使用**sp_configure**更新配置设置后, 系统管理员必须使用 "重新配置" 或 "使用替代重新配置" 来更新正在运行的配置值。 有关详细信息，请参阅“备注”部分。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|配置选项的名称。|  
|**最小值**|**int**|配置选项的最小值。|  
|**最大值**|**int**|配置选项的最大值。|  
|**config_value**|**int**|使用**sp_configure** (值为 "**值**") 设置配置选项的值。 有关这些选项的详细信息, 请参阅[服务器配置&#40;选项&#41; SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md)和[ &#40;sys.databases transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
|**run_value**|**int**|配置选项的当前运行值 ( **value_in_use**中的值)。<br /><br /> 有关详细信息, 请参阅[Sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
  
## <a name="remarks"></a>备注  
 使用**sp_configure**显示或更改服务器级设置。 若要更改数据库级别设置，请使用 ALTER DATABASE。 若要更改仅影响当前用户会话的设置，请使用 SET 语句。  
  
## <a name="updating-the-running-configuration-value"></a>更新运行的配置值  
 为某个*选项*指定新*值*时, 结果集将在**config_value**列中显示此值。 此值最初与**run_value**列中的值不同, 后者显示当前正在运行的配置值。 若要更新**run_value**列中的运行配置值, 系统管理员必须运行 "重新配置" 或 "重新配置替代"。  
  
 RECONFIGURE 和 RECONFIGURE WITH OVERRIDE 对每个配置选项都有效。 但是，基本 RECONFIGURE 语句会拒绝处于合理范围之外或可能导致选项冲突的任何选项值。 例如, 如果 "**恢复间隔**" 值大于60分钟或**关联掩码**值与**关联 i/o 掩码**值重叠, 则重新配置会生成错误。 与此相反，RECONFIGURE WITH OVERRIDE 则接受具有正确数据类型的任何选项值，并使用指定的值强制进行重新配置。  
  
> [!CAUTION]  
>  不合适的选项值会给服务器实例的配置造成不利影响。 请谨慎使用 RECONFIGURE WITH OVERRIDE。  
  
 RECONFIGURE 语句可以动态更新某些选项，而其他选项的更新则需要停止服务器再重新启动才能实现。 例如, "**最小服务器内存**" 和 " [!INCLUDE[ssDE](../../includes/ssde-md.md)]**最大服务器**内存" 服务器内存选项在中动态更新, 因此, 你可以更改它们而无需重新启动服务器。 与此相反, 重新配置**填充因子**选项的运行值需要重新启动[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 在配置选项上运行重新配置后, 可以通过执行**sp_configure '***option_name***'** 来查看是否已动态更新了选项。 **Run_value**和**config_value**列中的值应匹配动态更新选项。 还可以查看**sys.databases**目录视图的**is_dynamic**列, 查看哪些选项是动态的。  
 
 此更改也会写入 SQL Server 错误日志。
  
> [!NOTE]  
>  如果某个选项的指定*值*过高, 则**run_value**列将反映[!INCLUDE[ssDE](../../includes/ssde-md.md)]已默认为动态内存的事实, 而不是使用无效的设置。  
  
 有关详细信息, 请[参阅&#40;重新配置 transact-sql&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)。  
  
## <a name="advanced-options"></a>“高级选项”  
 某些配置选项 (如**关联掩码**和**恢复间隔**) 被指定为高级选项。 默认情况下，无法查看和更改这些选项。 若要使其可用, 请将**ShowAdvancedOptions**配置选项设置为1。  
  
 有关配置选项及其设置的详细信息, 请参阅[服务器配置选项&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要使用这两个参数来执行**sp_configure**来更改配置选项或运行重新配置语句, 您必须被授予 ALTER SETTINGS 服务器级别权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. 列出高级配置选项  
 以下示例显示如何设置并列出所有的配置选项。 先将 `show advanced option` 设置为 `1`，便可显示高级配置选项。 更改该选项后，不带参数执行 `sp_configure` 将会显示全部配置选项。  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 消息如下:"配置选项" 显示高级选项 "从0更改为1。 请运行 RECONFIGURE 语句进行安装。”  
  
 运行 `RECONFIGURE` 并显示全部配置选项：  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. 更改配置选项  
 以下示例将系统 `recovery interval` 设置为 `3` 分钟。  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. 列出所有可用的配置设置  
 以下示例显示如何列出所有的配置选项。  
  
```  
EXEC sp_configure;  
```  
  
 结果返回选项名称，后跟该选项的最小值和最大值。 **Config_value**是重新配置完成时[!INCLUDE[ssDW](../../includes/ssdw-md.md)]将使用的值。 **run_value** 是当前正在使用的值。 **config_value** 和 **run_value** 通常是相同的，除非该值正在进行更改。  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. 列出一个配置名称的配置设置  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. 设置 hadoop 连接  
 除了运行 sp_configure 外, 设置 Hadoop 连接还需要执行一些步骤。 有关完整过程, 请参阅[CREATE EXTERNAL DATA SOURCE &#40;transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
## <a name="see-also"></a>请参阅  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [软件 NUMA (SQL Server)](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
