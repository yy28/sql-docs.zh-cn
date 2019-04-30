---
title: 启动 SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 94466dc6c069ced5b2743cbd8a14d98271303477
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188863"
---
# <a name="start-sql-server-management-studio"></a>启动 SQL Server Management Studio
  开始本教程之前，让我们先来了解一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="opening-sql-server-management-studio"></a>打开 SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>打开 SQL Server Management Studio  
  
1.  上**启动**菜单，依次指向**所有程序**，指向[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]，然后单击**SQL Server Management Studio**。  
  
    > [!NOTE]  
    >  默认情况下不会安装 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 不可用，则运行安装程序安装此程序。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 不可用于 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express 是可作为从免费下载[Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=37075&clcid=0x409)，但具有不同的用户界面不是在本教程中所述。  
  
2.  在“连接到服务器”对话框中，确认默认设置，再单击“连接”。 若要连接，**服务器名称**框必须包含计算机的名称，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]是命名的实例，**服务器名称**框还应包含实例名称，格式\< *computer_name* > \\ <*instance_name*>。  
  
## <a name="management-studio-components"></a>Management Studio 组件  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 在专用于特定信息类型的窗口中显示信息。 数据库信息显示在对象资源管理器和文档窗口中。  
  
-   对象资源管理器是服务器中所有数据库对象的树视图。 此树视图可以包括 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的数据库。 对象资源管理器包括与其连接的所有服务器的信息。 打开 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]时，系统会提示您将对象资源管理器连接到上次使用的设置。 您可以在“已注册的服务器”组件中双击任意服务器进行连接，但无需注册要连接的服务器。  
  
-   文档窗口是 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的最大部分。 文档窗口可能包含查询编辑器和浏览器窗口。 默认情况下，将显示已与当前计算机上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例连接的“摘要”页。  
  
## <a name="showing-additional-windows"></a>显示其他窗口  
  
#### <a name="to-show-the-registered-servers-window"></a>显示“已注册的服务器”窗口  
  
1.  在“视图”菜单上，单击“已注册的服务器”。  
  
     “已注册的服务器”窗口将显示在对象资源管理器的上面。 “已注册的服务器”窗口列出的是经常管理的服务器。 可以在此列表中添加和删除服务器。 列出的服务器中仅包含运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 实例。  
  
2.  如果未显示你的服务器，在已注册的服务器，右键单击**数据库引擎**，然后单击**更新本地服务器注册**。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [与已注册的服务器和对象资源管理器连接](../object/object-explorer.md)  
  
  
