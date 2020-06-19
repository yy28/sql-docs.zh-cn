---
title: Microsoft 基于 COM 的冲突解决程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: a6637e4b-4e6b-40aa-bee6-39d98cc507c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b446c3300b2c8a440a092084f01c55105c9be95e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068666"
---
# <a name="microsoft-com-based-resolvers"></a>Microsoft COM-Based Resolvers
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 附带的所有基于 COM 的解决程序都处理更新冲突，并且在得到指示时，它们还会处理插入和删除冲突。 所有冲突解决程序都能处理列跟踪，大多数还能处理行跟踪。 这些冲突解决程序及所有其他基于 COM 的冲突解决程序都声明它们能处理的冲突类型，而合并复制代理使用默认的冲突解决程序处理所有其他冲突类型。  
  
 冲突解决程序在安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时安装。 可执行存储过程 **sp_enumcustomresolvers** 查看计算机上注册的所有冲突解决程序。 执行此过程将在一个单独的结果集中显示每个冲突解决程序的说明和全局唯一标识符 (GUID)。  
  
 若要指定冲突解决程序，请参阅 [Specify a Merge Article Resolver](../publish/specify-a-merge-article-resolver.md)。  
  
 下表说明了特定冲突解决程序的属性。  
  
|名称|要求的输入|说明|注释|  
|----------|--------------------|-----------------|--------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 累加性冲突解决程序|要求和的列的名称。 它必须为算术数据类型（例如 **int**、 **smallint**、 **numeric**等）。|冲突解决入选方由优先级值确定。 指定列的值设置为源列值与目标列值之和。 如果其中一列设置为 NULL，则结果按另一列的值设置。|只支持更新冲突和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平均化冲突解决程序|要平均化的列的名称。 它必须为算术数据类型（例如 **int**、 **smallint**、 **numeric**等）。|冲突解决入选方由优先级值确定。 所得列的值设置为源列值与目标列值的平均值。 如果其中一列设置为 NULL，则结果按另一列的值设置。|只支持更新冲突和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DATETIME（靠前首选）冲突解决程序|用于确定冲突解决入选方的列的名称。 它必须为 **datetime** 数据类型。|具有较早的 **datetime** 值的列确定冲突解决入选方。 如果其中一列设置为 NULL，则包含另一列的行为入选方。|支持更新冲突、行和列跟踪。 列值直接进行比较，并且不对不同的时区进行比较。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DATETIME（靠后首选）冲突解决程序|用于确定冲突解决入选方的列的名称。 它必须为 **datetime** 数据类型。|具有较晚的 **datetime** 值的列确定冲突解决入选方。 如果其中一列设置为 NULL，则包含另一列的行为入选方。|支持更新冲突、行和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 最大冲突解决程序|用于确定冲突解决入选方的列的名称。 它必须为算术数据类型（例如 **int**、 **smallint**、 **numeric**等）。|具有较大数值的列确定冲突解决入选方。 如果其中一列设置为 NULL，则包含另一列的行为入选方。|支持行和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 最小冲突解决程序|用于确定冲突解决入选方的列的名称。 它必须为算术数据类型（例如 **int**、 **smallint**、 **numeric**等）。|具有较小数值的列确定冲突解决入选方。 如果其中一列设置为 NULL，则包含另一列的行为入选方。|支持更新冲突、行和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 合并文本冲突解决程序|文本列的名称和分隔符，例如 `@resolver_info = '[col1][===]'`。|冲突解决入选方由优先级值确定。 冲突的文本列设置为合并值，该值的构成是：通用前缀，后面依次跟着发布服务器的特有部分、分隔符及订阅服务器的特有部分。|只支持更新冲突和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 首选订阅服务器冲突解决程序|无输入。|订阅服务器无论是作为源服务器还是目的服务器，始终是入选方。|支持所有冲突类型。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列优先冲突解决程序|用于确定冲突解决入选方的列的名称。 它必须为算术数据类型（例如 **int**、 **smallint**、 **numeric**等）。|具有较大数值的列确定冲突解决入选方。 如果其中一列设置为 NULL，则包含另一列的行为入选方。|支持更新冲突、行和列跟踪。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仅限上传冲突解决程序|无输入。|接受上载到发布服务器的更改；但更改不下载到订阅服务器。|支持所有冲突类型。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 仅限下载冲突解决程序|无输入。|拒绝上载到发布服务器的更改；但更改下载到订阅服务器。|支持所有冲突类型。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQL Server 存储过程冲突解决程序|冲突解决程序为处理冲突应调用的存储过程的名称。|冲突解决取决于在存储过程中指定的逻辑。|支持更新冲突。 有关详细信息，请参阅[为合并项目实现自定义冲突解决程序](../implement-a-custom-conflict-resolver-for-a-merge-article.md)|  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)   
 [sp_enumcustomresolvers (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)  
  
  
