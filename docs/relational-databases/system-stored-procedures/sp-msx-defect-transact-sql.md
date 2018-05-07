---
title: sp_msx_defect (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ffce49260f39c04665ec570e92a37e1783077dbe
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spmsxdefect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从多服务器操作中删除当前服务器。  
  
> [!CAUTION]  
>  **sp_msx_defect**编辑注册表。 建议不要手动编辑注册表，因为不适当或不正确的更改会导致严重的系统配置问题。 因此，只有有经验的用户才可以使用注册表编辑器程序编辑注册表。 有关详细信息，请参阅 Microsoft Windows 的文档。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>参数  
 [ **@forced_defection =**] *forced_defection*  
 指定是否强制脱离发生如果 Master SQLServerAgent 已永久丢失由于不可逆转地损坏**msdb**数据库，或否**msdb**数据库备份。 *forced_defection*是**位**，默认值为**0**，指示应发生，不强制的脱离。 值为**1**强制脱离。  
  
 通过执行强制脱离后**sp_msx_defect**，属于**sysadmin** Master SQLServerAgent 固定的服务器角色必须运行以下命令以完成该脱离操作：  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 当**sp_msx_defect**正确完成后，返回一条消息。  
  
## <a name="permissions"></a>权限  
 若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="see-also"></a>另请参阅  
 [sp_msx_enlist &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
