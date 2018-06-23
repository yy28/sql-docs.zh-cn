---
title: 从源代码管理中排除文件 |Microsoft 文档
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
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 597be5211a36e42320f3f7601c052121ef8aa2a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125679"
---
# <a name="exclude-files-from-source-control"></a>从源代码管理中排除文件
  如果你使用的解决方案包含不需要源代码管理服务的文件，则可以使用**从源代码管理中排除**命令以从源代码管理中排除的文件。 如果执行上述操作，这些被排除的文件仍会保留在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 数据库中，但不再随项目签入或签出。  
  
 应使用**从源代码管理中排除**命令仅在生成的文件上。 为生成的文件是指可以完全通过重新创建[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]基于解决方案中的另一个文件的内容。  
  
### <a name="to-exclude-a-file-from-source-control"></a>若要从源代码管理中排除文件  
  
1.  在解决方案资源管理器中，选择要排除的文件。  
  
2.  上**文件**菜单上，指向**源代码管理**，然后单击**排除** *\<文件名 >* **从源代码管理**。  
  
## <a name="see-also"></a>请参阅  
 [源控件基础知识](../../2014/database-engine/source-control-basics.md)   
 [设置源代码管理选项](../../2014/database-engine/set-source-control-options.md)   
 [更改源代码管理连接](../../2014/database-engine/change-source-control-connections.md)  
  
  