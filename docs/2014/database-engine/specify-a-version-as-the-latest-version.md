---
title: 指定的最新版本为版本 |Microsoft 文档
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
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 598fc6f2d90220f85cef590600d8fcf397384f28
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015942"
---
# <a name="specify-a-version-as-the-latest-version"></a>将版本指定为最新版本
  将文件签入源代码管理中时，您签入的版本会成为最新版本；签出或检索最新版本的用户将接收到最近签入项的本地副本。  
  
 但在某些情况下，您可能要把某项的早期版本指定为最新版本。 例如，您先签出文件、修改文件，然后又签入文件。 但后来又决定放弃所做的修改。 因为您已签入该项，所以不能选择撤消原来的签出。 在此情况下，可以将最初签出的版本指定为该项的最新版本。  
  
 指定最新版本的方法包括：  
  
-   **固定版本**。 驻留文件版本时，将不会删除比驻留版本更新的版本。 此外，可以对以前驻留的文件取消驻留。 执行此操作时，最近签入的文件版本将成为最新版本。 但不能签出已驻留的文件。  
  
-   **回滚到指定的版本**。 回滚到某版本时，将会从源代码管理中删除比所回滚版本更新的所有版本。 然后，您可以签出其余版本中的最新版本。  
  
### <a name="to-pin-a-version"></a>驻留版本  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，打开该解决方案。  
  
2.  在解决方案资源管理器中，选择要指定为最新版本的文件。  
  
3.  上**文件**菜单上，指向**源代码管理**单击**ViewHistory**。  
  
4.  在**的历史记录**\<文件 > 对话框框中，选择你想要指定为最新，然后单击版本**Pin**。  
  
     所选版本旁边会显示一个驻留符号，表示该版本是当前文件版本。 如果在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中加载了其他版本，则会提示您重新加载该文件。  
  
### <a name="to-roll-back-to-a-version"></a>回滚到某一版本  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，打开该解决方案。  
  
2.  在解决方案资源管理器中，选择要指定作为最新版本的项。  
  
3.  上**文件**菜单上，指向**源代码管理**单击**历史记录**。  
  
4.  在**历史记录选项**对话框中，单击**确定**以显示**文件历史记录**对话框。  
  
5.  在**文件历史记录**框中，选择你想要指定为最新版本，然后单击的版本**回滚**。  
  
     此时屏幕上显示一条消息，提示选定版本之后的所有版本都将被删除。  
  
6.  单击**是**回滚到所选版本。  
  
## <a name="see-also"></a>请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [签入文件](../../2014/database-engine/check-in-files.md)  
  
  