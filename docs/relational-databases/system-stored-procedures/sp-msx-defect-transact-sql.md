---
title: sp_msx_defect (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16e523bc26b8469f3ee7306f3e6fd2902ef727bb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528529"
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
`[ @forced_defection = ] forced_defection` 指定是否强制脱离 Master SQLServerAgent 永久丢失由于不可逆转地损坏如果，则发生**msdb**数据库中，或否**msdb**数据库备份。 *forced_defection*是**位**，默认值为**0**，指示应发生任何强制的脱离。 值为**1**强制进行脱离。  
  
 通过执行强制进行脱离后**sp_msx_defect**，属于**sysadmin** Master SQLServerAgent 上的固定的服务器角色必须运行以下命令以完成该脱离操作：  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 当**sp_msx_defect**正常完成后，返回一条消息。  
  
## <a name="permissions"></a>权限  
 若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="see-also"></a>请参阅  
 [sp_msx_enlist &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
