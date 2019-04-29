---
title: sp_mergecleanupmetadata (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6924ef36c57036cf6cad6e25a6dc5cebfa5fa5f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63017841"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  应仅在包含运行的版本的服务器的复制拓扑中使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早于[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 1。**sp_mergecleanupmetadata**允许管理员以进行中的元数据清除**MSmerge_genhistory**， **MSmerge_contents**和**MSmerge_tombstone**系统表。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，默认值为**%**，表示清除所有发布的元数据。 如果显式指定发布，则该发布必须已存在。  
  
`[ @reinitialize_subscriber = ] 'subscriber'` 指定是否重新初始化订阅服务器。 *订阅服务器上*是**nvarchar(5)**，可以是**TRUE**或**FALSE**，默认值为**TRUE**。 如果 **，则返回 TRUE**，订阅标记为重新初始化。 如果**FALSE**，未标记为要重新初始化订阅。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_mergecleanupmetadata**应仅在包含运行的版本的服务器的复制拓扑中使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早于[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 1。 仅包含 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 或更高版本的拓扑应使用基于元数据清理的自动保持功能。 运行此存储过程时，请注意运行此存储过程的计算机上的日志文件必然出现和可能出现的大小增长。  
  
> [!CAUTION]
>  之后**sp_mergecleanupmetadata**执行时，默认情况下，发布了元数据存储在订阅服务器上的所有订阅**MSmerge_genhistory**， **MSmerge_contents**并**MSmerge_tombstone**标记为要重新初始化，订阅服务器上任何挂起的更改都将丢失，并且当前快照将标记为已过时。  
> 
> [!NOTE]
>  如果有多个发布数据库，并且任何一个发布使用无限发布保持期 (**@retention**=**0**)，运行**sp_mergecleanupmetadata**不会清除合并复制更改跟踪数据库元数据。 因此，要谨慎使用无限发布保持。  
  
 执行此存储过程时，可以选择是否要重新初始化订阅服务器，通过设置**@reinitialize_subscriber**参数**TRUE** （默认值） 或**FALSE**. 如果**sp_mergecleanupmetadata**情况下执行**@reinitialize_subscriber**参数设置为**TRUE**，快照会重新应用于订阅服务器即使的订阅创建没有初始快照 （例如，如果快照数据和架构已手动应用，或在订阅服务器上已存在）。 将参数设置为**FALSE**应小心，因为如果不重新初始化发布，则必须确保发布服务器和订阅服务器上的数据同步。  
  
 而不考虑的值**@reinitialize_subscriber**， **sp_mergecleanupmetadata**失败是否存在正在进行的合并进程尝试将更改上载到发布服务器或在重新发布订阅服务器调用存储的过程的时间。  
  
 **执行 sp_mergecleanupmetadata 时设置与@reinitialize_subscriber= TRUE:**  
  
1.  建议（不是必需）停止对发布和订阅数据库的所有更新。 如果更新继续进行，则重新初始化发布时，上次合并后在订阅服务器上所做的所有更新都将丢失，但会保留数据收敛。  
  
2.  运行合并代理以执行合并。 我们建议你使用 **-验证**代理在每个订阅服务器上运行合并代理时的命令行选项。 如果运行的连续模式合并，请参阅*连续模式合并的特别注意事项*在本部分中更高版本。  
  
3.  完成所有合并后，请执行**sp_mergecleanupmetadata**。  
  
4.  执行**sp_reinitmergepullsubscription**上所有订阅服务器使用已命名或匿名请求订阅，以确保数据收敛。  
  
5.  如果运行的连续模式合并，请参阅*连续模式合并的特别注意事项*在本部分中更高版本。  
  
6.  为所有级别涉及的所有合并发布重新生成快照文件。 如果事先没有重新生成快照就试图合并，则会得到提示，要求您重新生成快照。  
  
7.  备份发布数据库。 如果没有这样做，会导致发布数据库还原后合并失败。  
  
 **执行 sp_mergecleanupmetadata 时设置与@reinitialize_subscriber= FALSE:**  
  
1.  停止**所有**发布和订阅数据库的更新。  
  
2.  运行合并代理以执行合并。 我们建议你使用 **-验证**代理在每个订阅服务器上运行合并代理时的命令行选项。 如果运行的连续模式合并，请参阅*连续模式合并的特别注意事项*在本部分中更高版本。  
  
3.  完成所有合并后，请执行**sp_mergecleanupmetadata**。  
  
4.  如果运行的连续模式合并，请参阅*连续模式合并的特别注意事项*在本部分中更高版本。  
  
5.  为所有级别涉及的所有合并发布重新生成快照文件。 如果事先没有重新生成快照就试图合并，则会得到提示，要求您重新生成快照。  
  
6.  备份发布数据库。 如果没有这样做，会导致发布数据库还原后合并失败。  
  
 **连续模式合并的特殊注意事项**  
  
 如果要运行连续模式合并，则必须执行以下两项操作之一：  
  
-   停止合并代理，然后执行另一个合并而无需 **-连续**指定的参数。  
  
-   停用与出版物**sp_changemergepublication**以确保任何正在轮询发布状态的连续模式合并失败。  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 完成后的步骤 3 中运行**sp_mergecleanupmetadata**，恢复连续模式合并基于在您停止的方式。 请使用以下两种方法之一：  
  
-   添加 **-连续**回合并代理参数。  
  
-   重新激活与该发布**sp_changemergepublication。**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_mergecleanupmetadata**。  
  
 若要使用此存储过程，发布服务器运行的必须是 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 订阅服务器必须运行下列任一[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 Service Pack 2。  
  
## <a name="see-also"></a>请参阅  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
