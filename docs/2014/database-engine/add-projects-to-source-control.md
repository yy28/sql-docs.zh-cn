---
title: 将项目添加到源代码管理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
caps.latest.revision: 27
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2fc1ae6eadef04ee183e5551a88ed480a696cf2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148268"
---
# <a name="add-projects-to-source-control"></a>将项目添加到源代码管理
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 解决方案可以承载多个脚本项目。 向源代码管理中添加项目的方式取决于项目所属的解决方案是否接受源代码管理。 如果解决方案处于源代码管理下，则签入解决方案时会自动向源代码管理中添加项目。 有关签入解决方案的详细信息，请参阅[在文件中检查](../../2014/database-engine/check-in-files.md)。  
  
 如果该项目所属的解决方案未处于源代码管理下，则可将该解决方案添加到源代码管理中，这样会自动添加解决方案的项目。 有关将解决方案添加到源代码管理的详细信息，请参阅[添加到源代码管理的解决方案](../../2014/database-engine/add-solutions-to-source-control.md)。  
  
 如果您不想要将解决方案添加到源代码管理，可以使用**将选定内容添加到源代码管理**命令手动添加项目。  
  
 数据库对象不直接受源代码管理提供程序的保护，但是可以创建数据库对象脚本并将脚本保存在源代码管理中。  
  
### <a name="to-add-a-project-to-source-control"></a>将项目添加到源代码管理  
  
1.  在解决方案资源管理器中，选择一个项目。  
  
2.  上**文件**菜单，依次指向**源代码管理**，然后单击**将所选项目添加到源代码管理**。  
  
    > [!NOTE]  
    >  如果您使用**将所选项目添加到源代码管理**命令添加属于源代码管理解决方案的项目时，系统会提示你是否想要将项目添加为受源代码管理解决方案的子文件夹，或添加将项目作为一个单独的文件夹。  
  
3.  如果出现提示，请登录到源代码管理提供程序。  
  
4.  **将添加到 SourceSafe 项目**对话框随即出现。 你的项目的名称显示在**项目**框。  
  
5.  在中**文件夹**列表中，打开你想要放置项目的文件夹。 或者，你可以单击**创建**若要创建一个文件夹中显示的名称与**项目**框。  
  
## <a name="see-also"></a>请参阅  
 [将解决方案和项目添加到源代码管理](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
