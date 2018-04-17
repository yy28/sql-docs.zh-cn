---
title: sp_configure (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 81e174922753ed4a40111caba8aa34efd359e866
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md)]

  显示或更改当前服务器的全局配置设置。

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
> [!NOTE]  
>  有关数据库级配置选项，请参阅[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要配置 SOFT-NUMA，请参阅[SOFT-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
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
 [ **@configname=** ] **'***option_name***'**  
 配置选项的名称。 *option_name* 的数据类型为 **varchar(35)**，默认值为 NULL。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]能够识别构成配置名称的任何唯一字符串。 如果未指定该参数，则返回选项的完整列表。  
  
 有关可用配置选项和其设置的信息，请参阅[服务器配置选项&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
 [ @configvalue= ] 'value'****  
 新的配置设置。 *value* 的数据类型为 **int**，默认值为 NULL。 最大值取决于各个选项。  
  
 若要查看每个选项的最大值，请参阅**最大**列**sys.configurations**目录视图。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 不带任何参数，在执行时**sp_configure**返回的结果集具有五个列和排序选项按字母顺序按升序排列下, 表中所示。  
  
 值**config_value**和**run_value**不自动等效。 在通过使用更新配置设置后**sp_configure**，系统管理员必须通过使用 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE 更新正在运行的配置值。 有关详细信息，请参见“备注”部分。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nvarchar(35)**|配置选项的名称。|  
|**最小值**|**int**|配置选项的最小值。|  
|**最大值**|**int**|配置选项的最大值。|  
|**config_value**|**int**|值配置选项已设置为使用**sp_configure** (中的值**sys.configurations.value**)。 有关这些选项的详细信息，请参阅[服务器配置选项&#40;SQL Server&#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md)和[sys.configurations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
|**run_value**|**int**|当前正在运行的配置选项的值 (中的值**sys.configurations.value_in_use**)。<br /><br /> 有关详细信息，请参阅[sys.configurations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
  
## <a name="remarks"></a>注释  
 使用**sp_configure**显示或更改服务器级设置。 若要更改数据库级别设置，请使用 ALTER DATABASE。 若要更改仅影响当前用户会话的设置，请使用 SET 语句。  
  
## <a name="updating-the-running-configuration-value"></a>更新运行的配置值  
 指定新*值*为*选项*，结果集会显示中的此值**config_value**列。 此值最初与中的值**run_value**列，显示当前正在运行的配置值。 若要更新在正在运行的配置值**run_value**列中，系统管理员必须运行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。  
  
 RECONFIGURE 和 RECONFIGURE WITH OVERRIDE 对每个配置选项都有效。 但是，基本 RECONFIGURE 语句会拒绝处于合理范围之外或可能导致选项冲突的任何选项值。 例如，如果 RECONFIGURE 产生一个错误**恢复间隔**值大于 60 分钟或如果**关联掩码**值与重叠**关联 I/O 掩码**值。 与此相反，RECONFIGURE WITH OVERRIDE 则接受具有正确数据类型的任何选项值，并使用指定的值强制进行重新配置。  
  
> [!CAUTION]  
>  不合适的选项值会给服务器实例的配置造成不利影响。 请谨慎使用 RECONFIGURE WITH OVERRIDE。  
  
 RECONFIGURE 语句可以动态更新某些选项，而其他选项的更新则需要停止服务器再重新启动才能实现。 例如，**最小服务器内存**和**最大服务器内存**动态在更新服务器内存选项[!INCLUDE[ssDE](../../includes/ssde-md.md)]; 因此，你可以更改它们无需重新启动服务器。 与此相反，重新配置的运行值**填充因子**选项需要重新启动[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 运行 RECONFIGURE 之后配置选项，你可以看到是否已动态更新选项通过执行**sp_configure'***option_name*****。 中的值**run_value**和**config_value**列应匹配动态更新选项。 你还可以检查以查看哪些选项是动态的通过查看**is_dynamic**列**sys.configurations**目录视图。  
  
> [!NOTE]  
>  如果指定*值*过高的选项， **run_value**列反映的情况是，[!INCLUDE[ssDE](../../includes/ssde-md.md)]已默认为动态内存，而不是使用不是有效的设置。  
  
 有关详细信息，请参阅[重新配置&#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)。  
  
## <a name="advanced-options"></a>“高级选项”  
 某些配置选项，如**关联掩码**和**恢复间隔**，指定为高级选项。 默认情况下，无法查看和更改这些选项。 若要使其可用，请设置**ShowAdvancedOptions**为 1 的配置选项。  
  
 有关配置选项和其设置的详细信息，请参阅[服务器配置选项&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行**sp_configure**与这两个参数来更改配置选项或运行 RECONFIGURE 语句，您必须被授予 ALTER SETTINGS 服务器级别权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. 列出高级配置选项  
 以下示例显示如何设置并列出所有的配置选项。 先将 `show advanced option` 设置为 `1`，便可显示高级配置选项。 更改该选项后，不带参数执行 `sp_configure` 将会显示全部配置选项。  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 以下是显示的消息：“配置选项 'show advanced options' 已从 0 改为 1。 请运行 RECONFIGURE 语句进行安装。”  
  
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
  
 结果返回选项名称，后跟该选项的最小值和最大值。 **Config_value**是值的[!INCLUDE[ssDW](../../includes/ssdw-md.md)]重新配置完成后，将使用。 **run_value** 是当前正在使用的值。 **config_value** 和 **run_value** 通常是相同的，除非该值正在进行更改。  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. 列出一个配置名称的配置设置  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. 设置 hadoop 连接  
 设置 Hadoop 连接需要除了运行 sp_configure 的几个步骤。 有关完整的过程中，请参阅[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE & #40;Transact SQL & #41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [软件 NUMA (SQL Server)](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
