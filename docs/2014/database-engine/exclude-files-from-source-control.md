---
title: 从源代码管理中排除文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9fb3c5ccb4fcaad062236eec6d04f995557dc2b8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933084"
---
# <a name="exclude-files-from-source-control"></a>从源代码管理中排除文件
  如果正在使用的解决方案包含不需要源代码管理服务的文件，则可以使用 "**从源代码管理中排除**" 命令从源代码管理中排除文件。 如果执行上述操作，这些被排除的文件仍会保留在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 数据库中，但不再随项目签入或签出。  
  
 只应在生成的文件上使用 "**从源代码管理中排除**" 命令。 生成的文件是指可以通过 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 解决方案中其他文件的内容完全重新创建的文件。  
  
### <a name="to-exclude-a-file-from-source-control"></a>从源代码管理中排除文件  
  
1.  在解决方案资源管理器中，选择要排除的文件。  
  
2.  在 "**文件**" 菜单上，指向 "**源代码管理**"，然后单击 " **Exclude** *\<file name>* **从源代码管理中**排除"。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理基础知识](../../2014/database-engine/source-control-basics.md)   
 [设置源代码管理选项](../../2014/database-engine/set-source-control-options.md)   
 [更改源代码管理连接](../../2014/database-engine/change-source-control-connections.md)  
  
  
