---
title: sp_delete_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 194395728e60f31c689293191be2cedca4d549f3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528909"
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从可用目标服务器列表中删除指定服务器。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>参数  
`[ @server_name = ] 'server'` 要删除作为可用目标服务器的服务器的名称。 *服务器*是**nvarchar(30)**，无默认值。  
  
`[ @clear_downloadlist = ] clear_downloadlist` 指定是否清除目标服务器的下载列表。 *clear_downloadlist*是类型**位**，默认值为**1**。 当*clear_downloadlist*是**1**，过程将删除服务器之前清除该服务器的下载列表。 当*clear_downloadlist*是**0**，不清除下载列表。  
  
`[ @post_defection = ] post_defection` 指定是否发布到目标服务器脱离指令。 *post_defection*是类型**位**，默认值为 1。 当*post_defection*是**1**，过程将在删除服务器之前向目标服务器脱离指令。 当*post_defection*是**0**，该过程不会发送到目标服务器脱离指令。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 若要删除目标服务器的常规方法是调用**sp_msx_defect**目标服务器上。 使用**sp_delete_targetserver**手动脱离时才需要。  
  
## <a name="permissions"></a>权限  
 若要运行此存储的过程，必须授予用户**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将从可用作业服务器中删除服务器 `LONDON1`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_help_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
