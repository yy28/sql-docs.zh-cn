---
title: 解决方案资源管理器源代码管理 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7165143ad238bbbeda14ac91f214f1410082beb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025502"
---
# <a name="solution-explorer-source-control"></a>解决方案资源管理器源代码管理
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 解决方案资源管理器可以集成到一个单独的源控制系统。 将解决方案或项目集成到源代码管理系统中后，即可控制针对项目中的脚本和查询的文件访问和版本控制。  
  
## <a name="solution-and-project-source-control"></a>解决方案和项目源代码管理  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 源代码管理是指以下系统：在该系统中，使用中心服务器软件存储和跟踪文件版本，并控制对文件的访问。 典型的源代码管理系统包括源代码管理提供程序以及两个或多个源代码管理客户端。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可与源代码管理服务集成在一起。 也就是说，可将该工具用作源代码管理提供程序的客户端。 您无需离开环境就可以轻松管理个人项目和团队项目。 源代码管理提供程序不包含在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中。  
  
#### <a name="to-select-a-source-control-provider"></a>选择源代码管理提供程序  
  
1.  安装源代码管理提供程序的客户端部分。  
  
2.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]的 **“工具”** 菜单中，单击 **“选项”**。  
  
3.  在**选项**对话框框中，展开**源代码管理**，然后单击**插件选择**页。  
  
4.  在**当前源代码管理插件**框中，选择源代码管理插件。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[源代码管理基础](../../2014/database-engine/source-control-basics.md)|定义基本源代码管理术语，并说明使用源代码管理服务，项目将如何从中受益。|  
|[将解决方案和项目添加到源代码管理](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|说明如何使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 环境，将解决方案和项目添加到源代码管理中。|  
|[从源代码管理打开解决方案和项目](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|说明如何使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 环境打开源代码管理的解决方案和项目。|  
|[管理签出](../../2014/database-engine/manage-checkouts.md)|说明如何从源代码管理中签出解决方案和文件。|  
|[管理签入](../../2014/database-engine/manage-checkins.md)|说明如何将解决方案和文件签入源代码管理。|  
|[设置和检索版本信息](../../2014/database-engine/set-and-retrieve-version-information.md)|说明如何检索项目或项的历史记录、检索项的本地副本或比较项的两个版本。|  
|||  
  
## <a name="see-also"></a>请参阅  
 [解决方案资源管理器](../ssms/solution/solution-explorer.md)   
 [解决方案&#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [项目&#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [用于管理解决方案和项目的文件](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  