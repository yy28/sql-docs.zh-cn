---
title: 分发数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f49e1f71897906d8ac3d947c43cd284cbee5289e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256663"
---
# <a name="distribution-database"></a>分发数据库
  分发数据库用于存储所有类型复制的元数据和历史记录数据，并存储事务复制的事务。  
  
 在许多情况下，单个分发数据库就能够满足需要。 不过，如果多个发布服务器使用单个分发服务器，则应考虑为每个发布服务器都创建一个分发数据库。 这样可确保通过每个分发数据库的数据流是不同的。 使用配置分发向导可以为分发服务器指定一个分发数据库。 如果需要，可以在 **“分发服务器属性”** 对话框中指定其他分发数据库。  
  
## <a name="options"></a>“常规”  
 **分发数据库名称**  
 为分发数据库输入名称。 分发数据库的默认名称为“distribution”。 如果您指定名称，名称最多可包含 128 个字符，在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中必须是唯一的，并且必须符合标识符的规则。 有关详细信息，请参阅 [Database Identifiers](../databases/database-identifiers.md)。  
  
 **分发数据库文件的文件夹** / **分发数据库日志文件的文件夹**  
 输入分发数据库和日志文件的路径。 这些路径必须指向分发服务器的本地磁盘，并以本地驱动器号和冒号（如 C：）开头。 映射的驱动器号和网络路径无效。  
  
> [!NOTE]  
>  通过将分发数据库日志放置在与分发数据库不同的磁盘驱动器上，可以减少事务写入操作所需的时间并提高复制的性能。  
  
## <a name="see-also"></a>请参阅  
 [“配置分发”](configure-distribution.md)   
 [配置发布和分发](configure-publishing-and-distribution.md)   
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)  
  
  
