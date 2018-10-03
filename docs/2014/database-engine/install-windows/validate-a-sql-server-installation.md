---
title: 验证 SQL Server 安装 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2a71d127ad565690f78dbbbf8eeffaa13194b2a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178557"
---
# <a name="validate-a-sql-server-installation"></a>验证 SQL Server 安装
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发现报告可用于验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本和在计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 **已安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能发现报告**显示的所有报表[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]， [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]产品和功能本地服务器上安装。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心的 **“工具”** 页上提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告。  
  
 **运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告：**  
  
 启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心，使用“开始”菜单，依次指向“所有程序”、“[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name>”、“配置工具”，然后单击“[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心”。 若要运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告，请在“[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心”的左侧导航区域中单击“工具”，然后单击“已安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告”。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发现报告将保存到 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< 上一安装会话\>。  
  
 您还可以通过命令行生成发现报告。 运行"Setup.exe /Action = RunDiscovery"在命令提示符下，如果添加"/ 问题与解答"到上述命令行，将显示没有 UI，但是仍将在 %programfiles%中创建报表\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< 上一安装会话\>。  
  
## <a name="see-also"></a>请参阅  
 [查看和读取 SQL Server 安装程序日志文件](view-and-read-sql-server-setup-log-files.md)  
  
  
