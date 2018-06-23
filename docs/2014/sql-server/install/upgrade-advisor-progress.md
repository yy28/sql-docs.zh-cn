---
title: 升级顾问进度 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e1b867360b773253ae22d24a76ce00b35c589d96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028491"
---
# <a name="upgrade-advisor-progress"></a>升级顾问进度
  升级顾问分析从对选定的各个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件执行分析的专用分析器开始。 分析完毕组件，如在报告进度**进度**对话框。  
  
## <a name="options"></a>“常规”  
 **操作**  
 指定选择来分析的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件。  
  
 **“状态”**  
 显示从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件进度界面返回的状态值。  
  
 **Message**  
 显示从各个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分析器返回的错误消息、失败消息或成功消息。  
  
> [!NOTE]  
>  如果分析时间过长，则可以停止分析，退出升级顾问分析向导，然后重新运行该向导。 若要缩短分析时间，请少选择一些组件来扫描。  
  
 分析完成后，报表将写入文件。 你可以通过单击查看报表**启动报表**以启动从该页报表查看器。 如果你想要在以后查看报表，则可以打开**升级顾问报表查看器**从升级顾问起始页。  
  
> [!NOTE]  
>  每次分析服务器后，都会保存先前的报表。 这些报表使用时间戳作为文件名进行保存。 报表查看器显示最近保存的五个报表。  
  
## <a name="see-also"></a>请参阅  
 [如何： 启动升级顾问](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [如何： 运行升级顾问分析向导](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [SQL Server 组件](../../../2014/sql-server/install/sql-server-components.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  