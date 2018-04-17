---
title: sp_copysubscription (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8a6a53bc7f9b793dfef4b685c4d55033657a152
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  不推荐使用可附加的订阅功能，未来的版本中将删除该功能。 在新的开发工作中不要使用此功能。 对于使用参数化筛选器分区的合并发布，建议您使用分区快照的新功能，这些功能可简化大量订阅的初始化。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。 对于未分区的发布，可以使用备份来初始化订阅。 有关详细信息，请参阅 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。  
  
 复制具有请求订阅但无推送订阅的订阅数据库。 仅可复制单个文件数据库。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>参数  
 [ **@filename =**] **'***file_name***'**  
 指定保存数据文件 (.mdf) 副本的完整路径（包括文件名）。 *文件名*是**nvarchar(260)**，无默认值。  
  
 [  **@temp_dir=**] *****temp_dir*****  
 包含临时文件的目录的名称。 *temp_dir*是**nvarchar(260)**，默认值为 NULL。 如果为 NULL， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，将使用默认数据目录。 该目录应有足够的空间可容纳具有保持所有组合的订阅服务器数据库文件大小的文件。  
  
 [  **@overwrite_existing_file=**] *****overwrite_existing_file*****  
 是可选的布尔型标志，用于指定是否覆盖现有文件中指定的相同名称的**@filename**。 *overwrite_existing_file*是**位**，默认值为**0**。 如果**1**，它将覆盖指定的文件**@filename**，如果它存在。 如果**0**，如果该文件存在，并且不覆盖该文件，存储的过程将失败。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_copysubscription**使用所有类型的复制来复制到文件中的订阅数据库，作为应用订阅服务器上的快照的替代方法。 必须将数据库配置为仅支持请求订阅。 具有相应权限的用户可制作订阅数据库的副本，然后将订阅文件 (.msf) 用电子邮件发送、复制或传输到另一个订阅服务器，这样它就可以作为订阅附加到该订阅服务器上。  
  
 要复制的订阅数据库的大小必须小于 2 GB。  
  
 **sp_copysubscription**仅支持的客户端订阅使用的数据库，并且如果数据库具有服务器订阅，无法执行。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_copysubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [备用快照文件夹位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
