---
title: 向源代码管理中添加解决方案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- adding solutions
- solutions [SQL Server Management Studio], adding
ms.assetid: b9e36569-616d-4e47-9140-0978a9bfe923
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1c72949fd8257332a36af52ab287ed326eed5274
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937318"
---
# <a name="add-solutions-to-source-control"></a>在源代码管理中添加解决方案
  将解决方案添加到源代码管理中时，通常需要添加整个解决方案及其包含的所有项目。 可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将解决方案添加到源代码管理中。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 项目完全驻留在本地磁盘上。 编辑、保存和生成项目均在本地进行。 将项目添加到源代码管理后，可以使用 "**签出**" 命令将项目的文件从源代码管理中签出。  
  
### <a name="to-add-a-solution-to-source-control"></a>将解决方案添加到源代码管理  
  
1.  在解决方案资源管理器中，选择要添加的解决方案。  
  
2.  在 "**文件**" 菜单上，指向 "**源代码管理**"，然后单击 "**将解决方案添加到源代码管理**"。  
  
3.  如果出现提示，请登录到源代码管理提供程序。  
  
4.  此时将显示 "**添加到 SourceSafe 项目**" 对话框。 项目的名称将显示在 "**项目**" 框中。  
  
5.  在 "**文件夹**" 列表中，打开要在其中放置项目的文件夹。 或者，您可以单击 "**创建**" 以创建一个文件夹，该文件夹的名称显示在 "**项目**" 框中。  
  
## <a name="see-also"></a>另请参阅  
 [将解决方案和项目添加到源代码管理](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)   
 [将项目添加到源代码管理](../../2014/database-engine/add-projects-to-source-control.md)  
  
  
