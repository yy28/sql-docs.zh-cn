---
title: 提供有关 SQL Server 2014 反馈 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sending feedback to Microsoft
- errors [SQL Server], feedback reporting
- feedback [SQL Server]
- submitting feedback [SQL Server]
- bug reporting [SQL Server]
- reporting usage information to Microsoft
- reporting errors to Microsoft
- SQL Server, feedback reporting
- documentation feedback [SQL Server]
- usage information reporting [SQL Server]
- product feedback [SQL Server]
- automatic error or usage reporting
ms.assetid: 28f3ebf0-ad71-4816-86a6-18a46f023cfe
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10466721f50dd8b090b5d6b1a06b5bffd6e5289d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62772273"
---
# <a name="providing-feedback-for-sql-server-2014"></a>提供有关 SQL Server 2014 的反馈
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 非常感谢您花费宝贵时间帮助我们改进 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 产品和文档。 您可以提供有关产品功能和用户界面的建议和错误报告，提交文档反馈，以及选择向 [!INCLUDE[msCoName](../includes/msconame-md.md)] 自动发送错误报告和使用情况数据以供分析。 此处分别介绍了以上三个反馈选项。  
  
## <a name="submitting-feedback-about-the-product"></a>提交有关产品的反馈  
 使用“[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 连接”上的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 反馈页发送有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能的建议和错误报告。 其中包括工具和实用工具、语言以及编程接口等功能。  
  
 您可以通过多种方式找到“[!INCLUDE[msCoName](../includes/msconame-md.md)] 连接”上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 反馈页。  
  
-   转到“[!INCLUDE[msCoName](../includes/msconame-md.md)] 连接”上的“[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 反馈”[网页](https://go.microsoft.com/fwlink/?linkid=34178)。  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“帮助”工具栏上，单击“发送反馈”按钮，或选择“社区/发送反馈”命令。  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的“帮助”工具栏上，单击“发送反馈”按钮。  
  
-   在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书中任意话题的顶部，单击“发送反馈”按钮。  
  
 在执行下列操作之前，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中不显示“帮助”工具栏：  
  
-   从实用工具访问“帮助”。  
  
-   选择**帮助**上的复选框**工具栏**选项卡**工具/自定义...** 命令。  
  
## <a name="automatic-error-and-usage-reporting"></a>自动报告错误和使用情况  
 可以将各个功能自动设置为报告错误并发送有关您如何使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 软件和服务的数据。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 将使用这些信息来改进 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 所有数据均保密。  
  
### <a name="managing-automatic-usage-reporting"></a>管理自动报告使用情况的功能  
 自动报告使用情况允许您决定是否收集数据并将数据发送给 [!INCLUDE[msCoName](../includes/msconame-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用两个管道来报告使用情况数据。 两个管道报告的数据相似，但报告的是不同程序的数据，并且可以分别打开或关闭。 打开或关闭使用其中任何一个程序的管道，将会停止或开始从共享同一个管道的其他程序收集数据。  
  
-   一个管道用于报告所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（联机丛书和 [!INCLUDE[msCoName](../includes/msconame-md.md)] 工具中某些基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Visual Studio 的用户界面元素除外）的使用情况数据。 安装之后，也可以关闭（或打开）此管道。 为此，在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，打开一个基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的项目，然后，从“帮助”菜单中选择“客户反馈选项”。 在您已经打开一个基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的项目之前，此命令不会出现。  
  
-   另一个管道用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具的基于 Visual Studio 的用户界面元素以及 Visual Studio。 安装之后，也可以关闭（或打开）此管道。 为此，在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，打开一个基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的项目，然后，从“帮助”菜单中选择“客户反馈选项”。 在您已经打开一个基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的项目之前，此命令不会出现。  
  
## <a name="helping-build-a-better-books-online"></a>有助于改进联机丛书  
 通过选择对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书启用使用情况报告功能，可以帮助开发小组不断改进文档。 我们收到的汇总数据有助于我们了解客户所需。 我们可以了解他们在主题之间的浏览方式、查看特定主题的频率，以及他们认为的最有用和最没有用的主题。  
  
 通过您的反馈信息，我们可以了解您使用文档的方式。 这有助于我们将文档撰写资源分配给最重要的主题，并且有助于为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 设计将来的文档系统。 来自联机丛书的此使用情况信息还可以帮助我们确定哪些是客户经常寻求帮助的功能。 这表明那些区域可能需要在可用性方面进行改进。  
  
  
