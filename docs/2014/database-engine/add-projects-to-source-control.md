---
title: 将项目添加到源代码管理 |Microsoft 文档
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
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f0c63dec978d50ef8544c86c6cc4811f55ef195
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129326"
---
# <a name="add-projects-to-source-control"></a>将项目添加到源代码管理
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 解决方案可以承载多个脚本项目。 向源代码管理中添加项目的方式取决于项目所属的解决方案是否接受源代码管理。 如果解决方案处于源代码管理下，则签入解决方案时会自动向源代码管理中添加项目。 有关在解决方案中检查的详细信息，请参阅[在文件中检查](../../2014/database-engine/check-in-files.md)。  
  
 如果该项目所属的解决方案未处于源代码管理下，则可将该解决方案添加到源代码管理中，这样会自动添加解决方案的项目。 有关将解决方案添加到源代码管理的详细信息，请参阅[将解决方案添加到源代码管理](../../2014/database-engine/add-solutions-to-source-control.md)。  
  
 如果您不想要将解决方案添加到源代码管理，则可以使用**将所选内容添加到源代码管理**命令手动添加项目。  
  
 数据库对象不直接受源代码管理提供程序的保护，但是可以创建数据库对象脚本并将脚本保存在源代码管理中。  
  
### <a name="to-add-a-project-to-source-control"></a>将项目添加到源代码管理  
  
1.  在解决方案资源管理器中，选择一个项目。  
  
2.  上**文件**菜单上，指向**源代码管理**，然后单击**添加选定的项目添加到源代码管理**。  
  
    > [!NOTE]  
    >  如果你使用**添加选定的项目添加到源代码管理**命令添加属于受源代码管理解决方案的项目时，提示你是否希望将该项目添加作为受源代码管理解决方案的子文件夹，还是希望添加该项目作为一个单独的文件夹。  
  
3.  如果出现提示，请登录到源代码管理提供程序。  
  
4.  **将添加到 SourceSafe 项目**对话框随即出现。 你的项目的名称显示在**项目**框。  
  
5.  在**文件夹**列表中，打开想要放置你的项目的文件夹。 或者，你可以单击**创建**若要创建的文件夹中显示的姓名**项目**框。  
  
## <a name="see-also"></a>请参阅  
 [将解决方案和项目添加到源代码管理](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  