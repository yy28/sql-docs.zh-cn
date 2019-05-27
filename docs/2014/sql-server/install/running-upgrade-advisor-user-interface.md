---
title: 运行升级顾问 （用户界面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5aecaea9bef359ad24aebbd20dd5e9547497043b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092444"
---
# <a name="running-upgrade-advisor-user-interface"></a>运行升级顾问（用户界面）
  在升级计划期间，可运行升级顾问来分析本地或远程组件。 升级顾问为分析的每个组件和实例生成一个报表。  
  
> [!IMPORTANT]  
>  升级顾问不分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的远程实例。 若要分析 [!INCLUDE[ssRS](../../includes/ssrs.md)] 实例，升级顾问必须安装在安装 [!INCLUDE[ssRS](../../includes/ssrs.md)] 的计算机上。  
>   
>  若要分析[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Integration Services，您必须具有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]安装和[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]安装在同一台计算机上。  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>运行升级顾问分析向导  
 运行升级顾问分析向导的过程包含以下六个步骤：  
  
1.  从升级顾问的起始页启动向导。  
  
2.  标识要分析的服务器和组件。  
  
3.  收集身份验证信息。  
  
4.  基于组件类型收集其他参数。  
  
5.  分析所选的组件。  
  
6.  生成升级问题的报告。  
  
 有关升级顾问分析向导的详细信息，请参阅[如何：运行升级顾问分析向导](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)。  
  
 为每个步骤所需的特定信息，请参阅[升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)。  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>运行升级顾问报表查看器  
 使用升级顾问报表查看器来查看由升级顾问分析向导生成的报表。 加载该报表后，可按照以下条件筛选报表内容：  
  
-   所有问题  
  
-   所有升级问题  
  
-   升级前的问题  
  
-   所有迁移问题  
  
-   已解决的问题  
  
-   未解决的问题  
  
 有关使用报表查看器的分步说明，请参阅以下主题：  
  
-   [如何：查看升级顾问报表](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [如何：筛选报表](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [如何：导出报表](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>请参阅  
 [如何：运行升级顾问分析向导](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [解决升级问题](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
