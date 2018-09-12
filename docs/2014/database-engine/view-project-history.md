---
title: 查看项目历史记录 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing project history
- version control services [SQL Server], project history
- projects [SQL Server Management Studio], historical information
- historical information [SQL Server], projects
ms.assetid: be0ea2ac-4a35-429c-9c9e-4001ea9035a4
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6b4000b1242a3c3efa720a6c7f8992f7aede472
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820623"
---
# <a name="view-project-history"></a>查看项目历史
  [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe (VSS) 项目的历史记录包括对每个项目文件执行的所有操作（包括文件创建、添加、删除和恢复）的列表。  
  
> [!NOTE]  
>  Visual SourceSafe 项目通常称为源代码管理服务器文件夹，它是服务器上存储源代码管理文件的服务器版本的存储位置。  
  
 可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 检查当前已加载解决方案所属的 Visual SourceSafe 项目的历史记录。 基于在项目历史记录中显示的信息，可以检索文件版本的本地副本，还原已删除的版本或在项目之间共享文件版本。  
  
### <a name="to-view-the-history-of-a-vss-project"></a>查看 VSS 项目的历史记录  
  
1.  在解决方案资源管理器中，选择项目。  
  
2.  上**文件**菜单，依次指向**源代码管理**然后单击**查看历史记录**。  
  
3.  在中**的历史记录**\<项目 > 对话框框中，执行以下操作之一：  
  
    -   查看所选文件的源代码管理系统副本。  
  
    -   查看有关所选文件的详细信息。  
  
    -   将所选文件检索到本地磁盘。  
  
    -   签出所选文件。  
  
    -   在两个源代码管理项目之间共享所选文件。  
  
    -   将历史记录报表导出到打印机、文件或剪贴板。  
  
## <a name="see-also"></a>请参阅  
 [设置和检索版本信息](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [查看文件状态](../../2014/database-engine/view-file-status.md)   
 [检索文件](../../2014/database-engine/retrieve-files.md)   
 [比较文件](../../2014/database-engine/compare-files.md)  
  
  
