---
title: 共享文件 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sharing files
- file sharing [SQL Server]
- version control services [SQL Server], file sharing
ms.assetid: 645f5c0a-e949-4e87-8988-85e4d6128464
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 528e0ac6eb185089fc7e5e38f654dd1acf2fb64e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127129"
---
# <a name="share-files"></a>共享文件
  可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 在各个源代码管理项目间共享一些项。 如果共享了某个项，则对该项的任何更改都会反映在共享该项的每个项目中。  
  
 项共享可为源代码管理用户带来下列好处：  
  
-   对于使用共享项的每个项目，不必单独存储一个该项的副本，从而可节省源代码管理客户端和服务器上的磁盘空间。 源代码管理提供程序将共享项存储在一个中央位置，共享该项的每个项目存储一个指向该位置的指针。  
  
-   避免了版本的不兼容性。 由于共享项的每个项目都使用相同版本的项，因此避免了在多个项目中独立更改项的每个副本时导致的冲突。  
  
### <a name="to-share-an-item"></a>共享一个项  
  
1.  在解决方案资源管理器中，选择要存放共享文件的文件夹或项目。  
  
2.  上**文件**菜单上，指向**源代码管理**，然后单击**共享**。  
  
3.  在**与共享**对话框中，浏览您想要共享，项目的目录列表，然后单击该项目。  
  
4.  单击**共享**。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理基础](../../2014/database-engine/source-control-basics.md)  
  
  