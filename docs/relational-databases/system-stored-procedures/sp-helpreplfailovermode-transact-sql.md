---
title: sp_helpreplfailovermode (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: baeb94873abbd243803166b478a1e5e95b12c3cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782025"
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示订阅的当前故障转移模式。 此存储过程在订阅服务器上对任何数据库执行。 有关故障转移模式的详细信息，请参阅[事务复制的可更新订阅](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher=**] **'***publisher***'**  
 参与该订阅服务器的更新的发布服务器的名称。 *发布服务器*是**sysname**，无默认值。 必须已为发布配置了发布服务器。  
  
 [  **@publisher_db =**] **'***publisher_db***’**  
 发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication=**] **'***publication***'**  
 参与该订阅服务器的更新的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***输出**  
 返回的故障转移模式的整数值并且是**输出**参数。 *failover_mode_id*是**tinyint**默认值为**0**。 它将返回**0**立即更新，并**1**进行排队更新。  
  
 [**@failover_mode=**] **'***failover_mode***输出**  
 返回在订阅服务器中修改数据所用的模式。 *failover_mode*是**nvarchar(10)** 默认值为 NULL。 是**输出**参数。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**立即**|立即更新：使用两阶段提交协议 (2PC)，将订阅服务器中的更新立即传播到发布服务器。|  
|**排入队列**|排队更新：将订阅服务器中的更新存储在队列中。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpreplfailovermode**进行哪些订阅启用即时更新并用排队更新作为故障转移时，发生故障时，快照复制或事务复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_helpreplfailovermode**。  
  
## <a name="see-also"></a>请参阅  
 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
