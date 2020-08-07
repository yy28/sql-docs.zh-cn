---
title: sp_add_category (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 323a86b4efbaa63d8858341c68908e30258d4889
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865285"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  将指定的作业、警报或操作员类别添加到服务器中。 有关替代方法，请参阅[使用 SQL Server Management Studio 创建作业类别](/sql/ssms/agent/create-a-job-category)。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > 在[AZURE SQL 托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)上，目前不支持所有 SQL Server 代理功能。 有关详细信息，请参阅[AZURE sql 托管实例与 SQL Server 的 t-sql 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>自变量  
`[ @class = ] 'class'`要添加的类别的类。 *类*是**varchar (8) ** ，其默认值为 JOB，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|JOB|添加作业类别。|  
|ALERT|添加警报类别。|  
|OPERATOR|添加操作员类别。|  
  
`[ @type = ] 'type'`要添加的类别的类型。 *类型*为**varchar (12) **，默认值为**LOCAL**，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|LOCAL|本地作业类别。|  
|多服务器|多服务器作业类别。|  
|无|除作业之外的类的类别 **。**|  
  
`[ @name = ] 'name'`要添加的类别的名称。 该名称在指定类中必须是唯一的。 *名称*为**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)   
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 必须从**msdb**数据库运行**sp_add_category** 。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_add_category**执行。  
  
## <a name="examples"></a>示例  
 以下示例将创建一个名为 `AdminJobs` 的本地作业类别。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_delete_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo.sys作业 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
