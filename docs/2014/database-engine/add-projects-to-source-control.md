---
title: 向源代码管理添加项目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: de32cbecdf132f1c881ab9fe5637af3a5c6cd400
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937348"
---
# <a name="add-projects-to-source-control"></a>将项目添加到源代码管理
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 解决方案可以承载多个脚本项目。 向源代码管理中添加项目的方式取决于项目所属的解决方案是否接受源代码管理。 如果解决方案处于源代码管理下，则签入解决方案时会自动向源代码管理中添加项目。 有关签入解决方案的详细信息，请参阅[签入文件](../../2014/database-engine/check-in-files.md)。  
  
 如果该项目所属的解决方案未处于源代码管理下，则可将该解决方案添加到源代码管理中，这样会自动添加解决方案的项目。 有关将解决方案添加到源代码管理的详细信息，请参阅[将解决方案添加到源代码管理](../../2014/database-engine/add-solutions-to-source-control.md)。  
  
 如果不想将解决方案添加到源代码管理，可以使用 "**将所选内容添加到源代码管理**" 命令手动添加项目。  
  
 数据库对象不直接受源代码管理提供程序的保护，但是可以创建数据库对象脚本并将脚本保存在源代码管理中。  
  
### <a name="to-add-a-project-to-source-control"></a>将项目添加到源代码管理  
  
1.  在解决方案资源管理器中，选择一个项目。  
  
2.  在 "**文件**" 菜单上，指向 "**源代码管理**"，然后单击 "**将所选项目添加到源代码管理**"。  
  
    > [!NOTE]  
    >  如果使用 "**将选定项目添加到源代码管理**" 命令添加属于源代码管理的解决方案的项目，系统将提示您是要将该项目添加为源代码管理的解决方案的子文件夹，还是将该项目添加为单独的文件夹。  
  
3.  如果出现提示，请登录到源代码管理提供程序。  
  
4.  此时将显示 "**添加到 SourceSafe 项目**" 对话框。 项目的名称将显示在 "**项目**" 框中。  
  
5.  在 "**文件夹**" 列表中，打开要在其中放置项目的文件夹。 或者，您可以单击 "**创建**" 以创建一个文件夹，该文件夹的名称显示在 "**项目**" 框中。  
  
## <a name="see-also"></a>另请参阅  
 [将解决方案和项目添加到源代码管理](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
