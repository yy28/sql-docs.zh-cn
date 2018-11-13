---
title: sp_showpendingchanges (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b520f2df23bfca8c3011cd3a171a92db272817e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709065"
---
# <a name="spshowpendingchanges-transact-sql"></a>sp_showpendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个结果集，其中显示了等待复制的更改。 此存储过程在发布服务器上的发布数据库中执行，或者在订阅服务器上的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  此过程提供近似的更改数以及这些更改所涉及到的行。 例如，此过程将从发布服务器或订阅服务器上检索信息，但是不会在这两个服务器上同时进行检索。 存储在其他节点上的信息产生的要同步的更改数可能比该过程估计的更改数小。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_showpendingchanges [ [ @destination_server = ] 'destination_server' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article']  
    [ , [ @show_rows = ] show_rows]  
```  
  
## <a name="arguments"></a>参数  
 [ @destination_server **=** ] **'***destination_server***’**  
 应用复制更改的服务器的名称。 *destination_server*是**sysname**，默认值为 NULL。  
  
 [ @publication **=** ] **'***发布***’**  
 发布的名称。 *发布*是**sysname**，默认值为 NULL。 当*发布*指定，则结果将限定为指定的发布。  
  
 [ @article **=** ] **'***文章***’**  
 项目的名称。 *文章*是**sysname**，默认值为 NULL。 当*一文*指定，则结果将限定为指定的项目。  
  
 [ @show_rows **=** ] *show_rows*  
 指定是否在结果集中挂起的更改，默认值为有关包含更多具体信息**0**。 如果值为**1**指定，则结果集包含 is_delete 和 rowguid 列。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|接收更改复制的服务器的名称。|  
|pub_name|**sysname**|发布的名称。|  
|destination_db_name|**sysname**|接收更改复制的数据库的名称。|  
|is_dest_subscriber|**bit**|指示要将更改复制到订阅服务器。 值为**1**指示到订阅服务器复制内容所做的更改。 **0**意味着更改复制到发布服务器。|  
|article_name|**sysname**|产生更改的表的项目名称。|  
|pending_deletes|**int**|等待复制的删除数。|  
|pending_ins_and_upd|**int**|等待复制的插入数和更新数。|  
|is_delete|**bit**|指示挂起更改是否为删除操作。 值为**1**指示更改为删除。 要求值为**1**为@show_rows。|  
|rowguid|**uniqueidentifier**|标识已更改的行的 GUID。 要求值为**1**为@show_rows。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 sp_showpendingchanges 用于合并复制。  
  
 sp_showpendingchanges 在排除合并复制故障时使用。  
  
 sp_showpendingchanges 的结果不包括第 0 代中的行。  
  
 为指定的项目*一文*不属于指定为发布*发布，* 为 pending_deletes 和 pending_ins_and_upd 返回计数 0。  
  
## <a name="permissions"></a>Permissions  
 只有 sysadmin 固定服务器角色的成员或 db_owner 固定数据库角色的成员才能执行 sp_showpendingchanges。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
