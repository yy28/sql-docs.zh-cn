---
title: 验证合并订阅服务器的分区信息 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication data validation [SQL Server replication], partitions
- parameterized filters [SQL Server replication], validating partition information
- validating partition information
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 057d3f820ac0f580a6109d5b5c04ea43e8eabd9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62507510"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>验证合并订阅服务器的分区信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在为合并发布定义参数化行筛选器时，将使用引用订阅服务器信息（如订阅服务器的登录名）的函数。 默认情况下，每次同步前和快照应用于订阅服务器时，复制都将根据此函数验证订阅服务器信息。 验证过程确保每个订阅服务器的数据都进行了正确的分区。 验证行为由 **validate_subscriber_info** 发布属性控制，此属性可以使用 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 或在“发布属性”对话框的“订阅选项”页上进行更改   。 有关更改发布属性的详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
## <a name="how-partition-validation-works"></a>分区验证的工作机制  
 对发布进行筛选时（例如，使用函数 **SUSER_SNAME()** ），合并代理根据对 **SUSER_SNAME()** 表达式有效的数据，将初始快照应用到每个订阅服务器。  
  
 如果验证已启用，则当订阅服务器重新连接到发布服务器进行下次同步处理时，合并代理将验证订阅服务器上的信息，并确保每个订阅服务器的分区与初始快照中所接收的相同。 针对每个后续合并或快照应用程序，合并代理将验证每个订阅服务器的分区。  
  
 如果合并代理检测到在筛选表达式中使用的函数返回了一个不同于其在初始快照中返回的值，则合并或快照应用程序将失败，而且此订阅服务器的订阅可能需要重新初始化。 可能需要重新初始化以避免出现问题（如果更改了订阅服务器的合并设置，则可能引发这些问题），不过，将订阅服务器上的信息更改回初始快照时使用的值（如登录名）可能也足以避免出现问题。  
  
 合并代理验证分区时，除了对筛选表达式使用的所有函数返回的值验证分区之外，代理还会检查快照的生成是否先于令其无效的更改，如元数据清除操作或架构更改。 如果分区快照太旧，合并代理将返回一个错误，并且必须根据当前常规快照为此订阅服务器重新生成分区快照。  
  
## <a name="see-also"></a>另请参阅  
 [复制管理常见问题解答](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [验证已复制的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
