---
title: 验证 SQL Server 安装 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e4c29cb28f76c930f1f04152528ca1a8a89dfc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775230"
---
# <a name="validate-a-sql-server-installation"></a>验证 SQL Server 安装
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发现报告可用于验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本和在计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 "**已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装的功能发现报告**" 显示在本地服务器[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]上[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]安装[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的所有[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、、、和产品和功能的报告。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心的 **“工具”** 页上提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告。  
  
 **运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告：**  
  
 使用“开始”菜单，依次指向“所有程序”、“[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  Version Name>”、“配置工具”，然后单击“**安装中心”，启动** 安装中心 **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\<**  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 。 若要运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能发现报告，请在“ **安装中心”** **的左侧导航区域中单击“工具”[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ，然后单击“已安装的  **功能发现报告”[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发现报告将保存到\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% ProgramFiles% \120\Setup Bootstrap\Log\\<上一个设置会话\>。  
  
 您还可以通过命令行生成发现报告。 如果将 "/q" 添加到上述命令行，请从命令提示符运行 "setup.exe/Action = RunDiscovery"。如果将 "/q" 添加到上述命令行，将不会显示任何 UI，\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]但仍\\将在% ProgramFiles\>% \120\Setup Bootstrap\Log<上一个设置会话中创建该报表。  
  
## <a name="see-also"></a>另请参阅  
 [查看和读取 SQL Server 安装程序日志文件](view-and-read-sql-server-setup-log-files.md)  
  
  
