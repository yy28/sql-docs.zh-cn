---
title: 源控件基础知识 |Microsoft 文档
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
- source controls [SQL Server Management Studio], providers
- source controls [SQL Server Management Studio]
- source controls [SQL Server Management Studio], about source controls
- source controls [SQL Server Management Studio], clients
ms.assetid: ca35b67a-104a-41fb-ac58-a61be06fe114
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5da8bd18f4ae5e62e5b9177a3ba76ac446bc1a6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024638"
---
# <a name="source-control-basics"></a>源代码管理基础
  源代码管理是指以下系统：在该系统中，使用中心服务器软件存储和跟踪文件版本，并控制对文件的访问。 典型的源代码管理系统包括源代码管理提供程序以及两个或多个源代码管理客户端。  
  
## <a name="source-control-benefits"></a>源代码管理的优点  
 如果将文件放置在源代码管理中，可以完成以下工作  
  
-   管理项的控制权在人员之间传递的过程。 源代码管理提供程序支持共享和独占文件访问。 如果对项目文件的访问是独占的，则源代码管理提供程序一次只允许一个用户签出文件并对其进行修改。 如果访问是共享的，则多个用户可以签出脚本文件。并且，源代码管理提供程序提供了一种机制，可以在各版本签入时对其进行合并。  
  
-   将连续版本的源代码管理项存档。 源代码管理提供程序可以存储将两个版本的源代码管理项区分开的数据。 提供程序将存储版本之间的差异，以及有关版本的重要信息：何时创建、何时修改，以及由谁创建。 几个人共同处理相同文件时，他们必须使用相同的代码页，以能够准确地比较版本。 因而，可以检索任何版本的源代码管理项。 还可以将任一版本指定为该项的最新版本。  
  
-   维护有关源代码管理项的历史和版本详细信息。 源代码管理可以存储项的创建日期和时间、签出或签入时间以及执行操作的用户。  
  
-   跨项目协作。 通过文件共享，多个项目可以共享源代码管理项。 某个共享项的更改将反映到共享该项的所有项目中。  
  
-   自动执行经常重复的源代码管理操作。 源代码管理提供程序可以在命令提示符中定义一个接口，用于支持源代码管理的主要功能。 可以在批处理文件中使用此接口，以实现自动定期执行源代码管理任务。  
  
-   从意外删除中恢复。 可以还原签入源代码管理的最新文件版本。  
  
-   节省源代码管理客户端和服务器上的磁盘空间。 有些源代码管理提供程序（如 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe）可以通过存储文件的最新版本以及各个版本与其前后版本之间的差异来节省服务器上的磁盘空间。 在客户端上，Visual SourceSafe 支持节省磁盘空间。 可以隐藏文件夹和文件，以便不将其下载到本地磁盘。  
  
 实际上，文件签出、签入和其他源代码管理操作都是通过源代码管理客户端（如 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]）完成的。 客户端能够与提供程序进行交互，以使提供程序的功能可用于一组分散的用户。 通过源代码管理客户端，用户可以浏览提供程序所存储的文件；添加和删除文件；签入和签出文件；以及检索本地文件的副本。  
  
> [!NOTE]  
>  本文档假定您使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 作为源代码管理提供程序。 如果使用的是其他源代码管理提供程序，您可能会发现本文档与正在运行的软件之间存在差异。 如果发现差异，请查阅源代码管理提供程序的文档。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**任务**|**主题**|  
|设置源代码管理选项|[设置源代码管理选项](../../2014/database-engine/set-source-control-options.md)|  
|更改源控件连接|[更改源代码管理连接](../../2014/database-engine/change-source-control-connections.md)|  
|从源代码管理中排除文件|[从源代码管理中排除文件](../../2014/database-engine/exclude-files-from-source-control.md)|  
  
  