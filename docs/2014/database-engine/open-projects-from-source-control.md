---
title: 从源代码管理打开项目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], opening
- opening projects
ms.assetid: 942f93a3-e264-4ec4-ba72-a28e0509a527
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec14f86b283fa8ccbc037feec4a8a54983126403
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774951"
---
# <a name="open-projects-from-source-control"></a>从源代码管理打开项目
  可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 直接从源代码管理打开项目。 执行此操作时，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将检索项目的最新版本，并将其复制到本地磁盘中。 此外，[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 环境还可以为项目自动创建一个解决方案。  
  
 从源代码管理打开一个项目后，可以签出和修改项目文件。  
  
> [!NOTE]  
>  下列过程只能使用一次。 此后，应打开其他任何项目一样项目 (通过单击**文件**，**打开**，然后**项目**)。  
  
### <a name="to-open-a-project-from-source-control"></a>从源代码管理打开项目  
  
1.  上**文件**菜单，依次指向**源代码管理**，然后单击**从源代码管理打开**。  
  
2.  如果出现提示，请登录到 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe。  
  
3.  在中**从 SourceSafe 创建本地项目**对话框框中，打开包含要打开的项目的文件夹。  
  
4.  **文件夹中创建一个新项目**框发生更改，以标识将在其中创建项目的本地目录。 如果你想要将项目放在不同的目录，键入目录或使用的路径**浏览**按钮以在本地磁盘上找到的目录。  
  
5.  在中**在文件夹对话框中创建新项目**，确认正确的文件夹已显示，然后单击**确定**。  
  
6.  在中**打开的解决方案**对话框框中，选择你想要打开，然后单击的项目**打开**。  
  
## <a name="see-also"></a>请参阅  
 [从源代码管理打开解决方案和项目](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)   
 [从源代码管理打开解决方案](../../2014/database-engine/open-solutions-from-source-control.md)  
  
  
