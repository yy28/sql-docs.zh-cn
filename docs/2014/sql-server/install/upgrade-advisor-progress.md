---
title: 升级顾问进度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 697f70d4435213a991e55adecb51a98120d8df1b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091555"
---
# <a name="upgrade-advisor-progress"></a>升级顾问进度
  升级顾问分析从对选定的各个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件执行分析的专用分析器开始。 分析组件时，将在 "**进度**" 对话框中报告进度。  
  
## <a name="options"></a>选项  
 **操作**  
 指定选择来分析的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件。  
  
 **状态**  
 显示从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件进度界面返回的状态值。  
  
 **消息**  
 显示从各个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分析器返回的错误消息、失败消息或成功消息。  
  
> [!NOTE]  
>  如果分析时间过长，则可以停止分析，退出升级顾问分析向导，然后重新运行该向导。 若要缩短分析时间，请少选择一些组件来扫描。  
  
 分析完成后，报表将写入文件。 您可以通过单击 "**启动报表**" 从此页启动报表查看器来查看报表。 如果以后要查看报表，可以从升级顾问起始页打开**升级顾问报表查看器**。  
  
> [!NOTE]  
>  每次分析服务器后，都会保存先前的报表。 这些报表使用时间戳作为文件名进行保存。 报表查看器显示最近保存的五个报表。  
  
## <a name="see-also"></a>另请参阅  
 [如何启动升级顾问](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [如何：运行升级顾问分析向导](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [SQL Server 组件](../../../2014/sql-server/install/sql-server-components.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
