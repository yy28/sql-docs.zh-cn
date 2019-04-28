---
title: 设置和检索版本信息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- historical information [SQL Server]
- source controls [SQL Server Management Studio], version information
- retrieving version information
- current file version information
- version control services [SQL Server], retrieving version information
- version control services [SQL Server], setting version information
- status information [SQL Server], source control files
- historical information [SQL Server], source control files
ms.assetid: c3f253c4-4e3d-48e8-8d90-bd6ee899faf7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68113c6de003aea94924f6e220373664212becf1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843478"
---
# <a name="set-and-retrieve-version-information"></a>设置和检索版本信息
  版本信息包括源代码管理的文件的历史记录和当前状态。 对于每个源代码管理的文件，[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 都将会维护其全面的历史记录，这样，您就可以跟踪一个或多个文件随时间变化的情况。 还可以使用该信息检索任何文件版本的本地副本，或比较任何两个文件版本。  
  
 文件的历史记录包括：  
  
-   版本号，用来标识该版本在相同文件的其他版本中的序列。  
  
-   已执行的操作。 跟踪的操作包括文件创建、签入和删除。  
  
-   执行涉及该文件操作的人员的用户名。  
  
-   执行操作时的日期和时间。  
  
 Visual SourceSafe 还维护有关当前已加载解决方案的当前状态信息。 该信息提供了文件当前状态的快照，包括：  
  
-   签出文件的用户标识。  
  
-   所选文件的最新版本号。  
  
-   版本的创建日期。  
  
-   与版本关联的用户注释。  
  
-   用于共享文件的项目的路径。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [查看文件历史记录](../../2014/database-engine/view-file-history.md)  
  
-   [查看项目历史记录](../../2014/database-engine/view-project-history.md)  
  
-   [查看文件状态](../../2014/database-engine/view-file-status.md)  
  
-   [检索文件](../../2014/database-engine/retrieve-files.md)  
  
-   [将某个版本指定为最新版本](../../2014/database-engine/specify-a-version-as-the-latest-version.md)  
  
-   [比较文件](../../2014/database-engine/compare-files.md)  
  
-   [共享文件](../../2014/database-engine/share-files.md)  
  
-   [创建历史记录和状态报表](../../2014/database-engine/create-history-and-status-reports.md)  
  
## <a name="see-also"></a>请参阅  
 [源代码管理基础](../../2014/database-engine/source-control-basics.md)  
  
  
