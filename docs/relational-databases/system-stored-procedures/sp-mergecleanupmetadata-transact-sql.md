---
title: sp_mergecleanupmetadata (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 026675528003028ffd3fd73301f47f75bcab0575
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33002154"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  应仅在包括运行的版本的服务器的复制拓扑中使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 1。**sp_mergecleanupmetadata**允许管理员以清除元数据中**MSmerge_genhistory**， **MSmerge_contents**和**MSmerge_tombstone**系统表。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication =** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，默认值为**%**，这会清理所有发布的元数据。 如果显式指定发布，则该发布必须已存在。  
  
 [  **@reinitialize_subscriber =** ] *****订阅服务器*****  
 指定是否重新初始化订阅服务器。 *订阅服务器*是**nvarchar(5)**，可以是**TRUE**或**FALSE**，默认值为**TRUE**。 如果**TRUE**，订阅标记为重新初始化。 如果**FALSE**，订阅不会标记为重新初始化。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_mergecleanupmetadata**应仅在包括运行的版本的服务器的复制拓扑中使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 1。 仅包含 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 或更高版本的拓扑应使用基于元数据清理的自动保持功能。 运行此存储过程时，请注意运行此存储过程的计算机上的日志文件必然出现和可能出现的大小增长。  
  
> [!CAUTION]  
>  后**sp_mergecleanupmetadata**执行时，默认情况下，订阅服务器上的已存储在元数据的发布的所有订阅**MSmerge_genhistory**， **MSmerge_contents**和**MSmerge_tombstone**标记为重新初始化订阅服务器上任何挂起的更改都将丢失，并且当前快照标记为已过时。  
  
> [!NOTE]  
>  如果有多个发布上一个数据库，并且这些发布的任何一个使用无限发布保持期 (**@retention**=**0**)，运行**sp_mergecleanupmetadata**不清除合并复制更改跟踪的数据库的元数据。 因此，要谨慎使用无限发布保持。  
  
 时执行此存储过程，你可以选择是否通过设置重新初始化订阅服务器**@reinitialize_subscriber**参数**TRUE** （默认值） 或**FALSE**. 如果**sp_mergecleanupmetadata**执行时使用**@reinitialize_subscriber**参数设置为**TRUE**，快照会重新应用于订阅服务器即使订阅已创建没有初始快照 （例如，如果快照数据和架构已手动应用或订阅服务器上已存在）。 将参数设置为**FALSE**应多加小心，因为如果发布不重新初始化订阅，则必须确保发布服务器和订阅服务器上的数据同步。  
  
 无论的值如何**@reinitialize_subscriber**， **sp_mergecleanupmetadata**失败，如果有正在进行合并尝试将更改上载到发布服务器或在重新发布订阅服务器的进程调用存储的过程的时间。  
  
 **执行与 sp_mergecleanupmetadata @reinitialize_subscriber = TRUE:**  
  
1.  建议（不是必需）停止对发布和订阅数据库的所有更新。 如果更新继续进行，则重新初始化发布时，上次合并后在订阅服务器上所做的所有更新都将丢失，但会保留数据收敛。  
  
2.  运行合并代理以执行合并。 我们建议你使用 **– 验证**在每个订阅服务器上时运行合并代理的代理命令行选项。 如果你正在运行连续模式合并，请参阅*连续模式下合并的特殊注意事项*本部分中更高版本。  
  
3.  所有合并都完成后，执行**sp_mergecleanupmetadata**。  
  
4.  执行**sp_reinitmergepullsubscription**使用已命名或匿名请求订阅，以确保数据收敛的所有订阅服务器上。  
  
5.  如果你正在运行连续模式合并，请参阅*连续模式下合并的特殊注意事项*本部分中更高版本。  
  
6.  为所有级别涉及的所有合并发布重新生成快照文件。 如果事先没有重新生成快照就试图合并，则会得到提示，要求您重新生成快照。  
  
7.  备份发布数据库。 如果没有这样做，会导致发布数据库还原后合并失败。  
  
 **执行与 sp_mergecleanupmetadata @reinitialize_subscriber = FALSE:**  
  
1.  停止**所有**发布和订阅数据库的更新。  
  
2.  运行合并代理以执行合并。 我们建议你使用 **– 验证**在每个订阅服务器上时运行合并代理的代理命令行选项。 如果你正在运行连续模式合并，请参阅*连续模式下合并的特殊注意事项*本部分中更高版本。  
  
3.  所有合并都完成后，执行**sp_mergecleanupmetadata**。  
  
4.  如果你正在运行连续模式合并，请参阅*连续模式下合并的特殊注意事项*本部分中更高版本。  
  
5.  为所有级别涉及的所有合并发布重新生成快照文件。 如果事先没有重新生成快照就试图合并，则会得到提示，要求您重新生成快照。  
  
6.  备份发布数据库。 如果没有这样做，会导致发布数据库还原后合并失败。  
  
 **连续模式下合并的特殊注意事项**  
  
 如果要运行连续模式合并，则必须执行以下两项操作之一：  
  
-   停止合并代理，然后执行另一个合并而无需 **-连续**指定参数。  
  
-   停用与发布**sp_changemergepublication**以确保发布状态轮询任何连续模式合并失败。  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 已完成时的步骤 3 中运行**sp_mergecleanupmetadata**，恢复基于停止它们的连续模式合并。 请使用以下两种方法之一：  
  
-   添加 **– 连续**回合并代理参数。  
  
-   重新激活与发布**sp_changemergepublication。**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_mergecleanupmetadata**。  
  
 若要使用此存储过程，发布服务器运行的必须是 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 订阅服务器必须运行下列任一[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0，Service Pack 2。  
  
## <a name="see-also"></a>另请参阅  
 [MSmerge_genhistory &#40;Transact SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
