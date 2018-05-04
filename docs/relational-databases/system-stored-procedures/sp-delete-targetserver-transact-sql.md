---
title: sp_delete_targetserver (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fa60536c79e9c88bc3b67e361260d96b87b0984
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
 [ **@server_name=** ] **'***server***'**  
 要作为可用目标服务器来删除的服务器的名称。 *服务器*是**nvarchar (30)**，无默认值。  
  
 [  **@clear_downloadlist=** ] *clear_downloadlist*  
 指定是否清除目标服务器的下载列表+。 *clear_downloadlist*是类型**位**，默认值为**1**。 当*clear_downloadlist*是**1**，过程删除服务器之前，清除服务器的下载列表。 当*clear_downloadlist*是**0**，下载列表不会清除。  
  
 [  **@post_defection=** ] *post_defection*  
 指定是否向目标服务器发布脱离指令。 *post_defection*是类型**位**，默认值为 1。 当*post_defection*是**1**，该过程将发送到目标服务器之前删除服务器缺陷指令。 当*post_defection*是**0**，该过程不会发送到目标服务器的缺陷指令。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 若要删除目标服务器的正常方式是调用**sp_msx_defect**目标服务器上。 使用**sp_delete_targetserver**手动脱离时才有必要。  
  
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
 [sp_help_targetserver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
