---
title: 生成 SQL 脚本（复制对象）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 99bd088d8d79da34c00b688380b76eda8b56de08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128299"
---
# <a name="generate-sql-script-replication-objects"></a>生成 SQL 脚本（复制对象）
  复制脚本包含实现已编写脚本的复制组件（如发布或订阅）所需的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系统存储过程。 制订灾难恢复计划时，应要求对拓扑中的所有复制组件编写脚本，另外，脚本还可以用来自动处理重复性的任务。 复制提供了两个对话框用以编写复制对象的脚本：  
  
-   **“生成 SQL 脚本”** 对话框，可以在 **msCoName** 中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]文件夹和所有子文件夹的上下文菜单中找到。 使用此对话框，可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上编写所有复制对象的脚本。  
  
-   **生成 SQL 脚本 \<对象名称>**，可以在发布和订阅的上下文菜单中找到。 使用此对话框，可以编写单个对象的脚本。  
  
 这些对话框在单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上编写对象脚本；并不连接到其他实例编写相关对象的脚本。  
  
## <a name="generate-sql-script-options"></a>生成 SQL 脚本选项  
 **分发服务器属性**  
 选择此选项可编写存储过程脚本以执行以下操作：启用或禁用分发服务器；添加或删除与分发服务器相关联的发布服务器；创建或删除分发数据库。  
  
 **下列数据源中的发布**  
 选择此选项可编写存储过程脚本以执行以下操作：启用或禁用发布；以及创建或删除发布、项目、推送订阅和复制作业。  
  
 **下列数据源中的订阅**  
 选择此项将编写存储过程脚本，以创建或删除请求订阅和复制作业。  
  
 **“用于创建或启用组件”** 和 **“用于删除或禁用组件”**  
 指定脚本是否应包含用于创建或删除复制对象的命令。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用此对话框创建一组用于启用和禁用组件的脚本。  
  
 **复制作业**  
 选择此项将编写复制作业脚本（除编写存储过程调用脚本之外）。 只有在分发服务器中编写脚本时，此选项才可用。  
  
 在执行复制存储过程时将创建必需的作业，因此不需要选择此选项。 不过，在必须重新创建单个作业时，创建作业记录还是有用的。  
  
## <a name="generate-sql-script-objectname-options"></a>“生成 SQL 脚本 \<对象名称>”选项  
 **“用于创建或启用组件”** 和 **“用于删除或禁用组件”**  
 指定脚本是否应包含用于创建或删除复制对象的命令。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用此对话框来创建一组用于启用和禁用组件的脚本。  
  
 **复制作业**  
 只有在 **“生成 SQL 脚本”** 对话框中，此选项才可用。  
  
## <a name="see-also"></a>请参阅  
 [编写复制脚本](scripting-replication.md)  
  
  