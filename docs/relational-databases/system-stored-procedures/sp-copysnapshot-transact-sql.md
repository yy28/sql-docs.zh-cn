---
title: sp_copysnapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysnapshot
- sp_copysnapshot_TSQL
helpviewer_keywords:
- sp_copysnapshot
ms.assetid: a012a32f-6f26-45bf-8046-b51cd7fec455
author: stevestein
ms.author: sstein
ms.openlocfilehash: 30e96ad145abdb123e5bc5540f74f23251d1a69e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768892"
---
# <a name="spcopysnapshot-transact-sql"></a>sp_copysnapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  将指定发布的快照文件夹复制到中 **@destination_folder** 列出的文件夹。 此存储过程在发布服务器上对发布数据库执行。 此存储过程用于将快照复制到可移动介质（如 CD-ROM）上。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_copysnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'`要复制其快照内容的发布的名称。 *发布*为**sysname**, 无默认值。  
  
`[ @destination_folder = ] 'destination_folder'`是要将发布快照内容复制到其中的文件夹的名称。 *destination_folder*的值为**nvarchar (255)** , 无默认值。 *Destination_folder*可以是备用位置, 如在其他服务器、网络驱动器或可移动介质 (如 cd-rom 或可移动磁盘) 上。  
  
`[ @subscriber = ] 'subscriber'`订阅服务器的名称。 *订阅服务器*的值为 sysname, 默认值为 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'`订阅数据库的名称。 *subscriber_db*的值为 sysname, 默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)  
  
## <a name="remarks"></a>备注  
 **sp_copysnapshot**用于所有类型的复制。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本7.0 及更早版本的订阅服务器不能使用备用快照位置。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_copysnapshot**。  
  
## <a name="see-also"></a>请参阅  
 [备用快照文件夹位置](../../relational-databases/replication/snapshot-options.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
