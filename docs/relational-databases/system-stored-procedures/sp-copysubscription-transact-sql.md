---
title: sp_copysubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
author: stevestein
ms.author: sstein
ms.openlocfilehash: 71027fb060a5085289aed4c8a637bc76a71bbd2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108682"
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  不推荐使用可附加的订阅功能，未来的版本中将删除该功能。 在新的开发工作中不要使用此功能。 对于使用参数化筛选器分区的合并发布，建议您使用分区快照的新功能，这些功能可简化大量订阅的初始化。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。 对于未分区的发布，可以使用备份来初始化订阅。 有关详细信息，请参阅 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。  
  
 复制具有请求订阅但无推送订阅的订阅数据库。 仅可复制单个文件数据库。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>参数  
`[ @filename = ] 'file_name'` 是指定的完整路径，包括文件名称，数据文件 (.mdf) 的副本保存到的字符串。 *文件名*是**nvarchar(260)** ，无默认值。  
  
`[ @temp_dir = ] 'temp_dir'` 是包含临时文件的名称。 *temp_dir*是**nvarchar(260)** ，默认值为 NULL。 如果为 NULL， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将使用默认数据目录。 该目录应有足够的空间可容纳具有保持所有组合的订阅服务器数据库文件大小的文件。  
  
`[ @overwrite_existing_file = ] 'overwrite_existing_file'` 可选布尔标志，该标志指定是否覆盖现有文件中指定的同名 **@filename** 。 *overwrite_existing_file*是**位**，默认值为**0**。 如果**1**，它将覆盖指定的文件 **@filename** ，如果它存在。 如果**0**，如果该文件存在，并且不覆盖该文件存储的过程将失败。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_copysubscription**用于所有类型的复制将订阅数据库复制到一个文件作为应用于订阅服务器上的快照的替代方法。 必须将数据库配置为仅支持请求订阅。 具有相应权限的用户可制作订阅数据库的副本，然后将订阅文件 (.msf) 用电子邮件发送、复制或传输到另一个订阅服务器，这样它就可以作为订阅附加到该订阅服务器上。  
  
 要复制的订阅数据库的大小必须小于 2 GB。  
  
 **sp_copysubscription**仅具有客户端订阅的数据库支持，并且数据库具有服务器订阅时不能执行。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_copysubscription**。  
  
## <a name="see-also"></a>请参阅  
 [备用快照文件夹位置](../../relational-databases/replication/snapshot-options.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
