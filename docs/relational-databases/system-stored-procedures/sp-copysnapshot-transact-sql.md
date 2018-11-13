---
title: sp_copysnapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_copysnapshot
- sp_copysnapshot_TSQL
helpviewer_keywords:
- sp_copysnapshot
ms.assetid: a012a32f-6f26-45bf-8046-b51cd7fec455
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0400d0f91e3b0b44b7eae603f8cc910230288f34
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746505"
---
# <a name="spcopysnapshot-transact-sql"></a>sp_copysnapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将指定的发布的快照文件夹复制到文件夹中列出**@destination_folder**。 在发布服务器上对发布数据库执行此存储的过程。 此存储过程用于将快照复制到可移动介质（如 CD-ROM）上。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_copysnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 将复制其快照内容的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@destination_folder=**] **'***destination_folder*****  
 是的发布快照内容要复制的名称。 *destination_folder*是**nvarchar(255)**，无默认值。 *Destination_folder*可以如另一台服务器、 网络驱动器或可移动媒体 （如 Cd-rom 或可移动磁盘） 的备用位置。  
  
 [ **@subscriber=**] **'***订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*数据类型为 sysname，默认值为 NULL。  
  
 [ **@subscriber_db=**] **'***subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*数据类型为 sysname，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_copysnapshot**用于所有类型的复制。 运行订阅服务器[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本 7.0 和更早版本不能使用备用快照位置。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_copysnapshot**。  
  
## <a name="see-also"></a>请参阅  
 [备用快照文件夹位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
