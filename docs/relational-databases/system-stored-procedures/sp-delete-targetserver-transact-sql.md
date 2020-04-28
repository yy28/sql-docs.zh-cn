---
title: sp_delete_targetserver （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 487d88a7580432bf947893920d307e2f0adffd18
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68111995"
---
# <a name="sp_delete_targetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从可用目标服务器列表中删除指定服务器。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>参数  
`[ @server_name = ] 'server'`要作为可用目标服务器删除的服务器的名称。 *服务器*为**nvarchar （30）**，无默认值。  
  
`[ @clear_downloadlist = ] clear_downloadlist`指定是否清除目标服务器的下载列表。 *clear_downloadlist*的类型为**bit**，默认值为**1**。 当*clear_downloadlist*为**1**时，过程将在删除服务器之前清除服务器的下载列表。 如果*clear_downloadlist*为**0**，则不会清除下载列表。  
  
`[ @post_defection = ] post_defection`指定是否将缺陷指令发布到目标服务器。 *post_defection*的类型为**bit**，默认值为1。 当*post_defection*为**1**时，过程将在删除服务器之前向目标服务器发布缺陷指令。 当*post_defection*为**0**时，该过程不会将缺陷指令发布到目标服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 删除目标服务器的常规方法是在目标服务器上调用**sp_msx_defect** 。 仅当需要手动脱离时才使用**sp_delete_targetserver** 。  
  
## <a name="permissions"></a>权限  
 若要运行此存储过程，用户必须被授予**sysadmin**固定服务器角色。  
  
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
 [sp_help_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
