---
title: 检索文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], file retrieval
- file retrieval [SQL Server]
- retrieving files
ms.assetid: 37b74426-e262-43b2-a81f-79b1fd1a36ec
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 548fac7dbc7d1f2750a130da9847be406361d8bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149537"
---
# <a name="retrieve-files"></a>检索文件
  打开源代码管理的项目后，可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将项目文件的本地副本从源代码管理存储区检索到项目所在的本地目录中。  
  
 可以通过以下方法使用集成的源代码管理检索文件：  
  
-   **获取最新版本 （递归）** 命令  
  
     检索选定文件的最新签入版本。 如果选择了解决方案或项目，则此命令将检索所有解决方案和项目文件的最新版本。  
  
-   **获取**命令  
  
     显示**获取**对话框中，可以使用以检索所选文件的最新版本或检索选定的解决方案或项目中的文件的子集。  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>检索项目中所有文件的最新版本  
  
1.  在解决方案资源管理器中，选择项目。  
  
2.  上**文件**菜单，依次指向**源代码管理**，然后单击**获取最新版本 （递归）**。  
  
 项目中文件的最新版本将被检索到本地磁盘上的项目位置。  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>只检索项目中的某些文件  
  
1.  在解决方案资源管理器中，选择要检索的项。  
  
2.  上**文件**菜单，依次指向**源代码管理**，然后单击**获取**。  
  
3.  在中**获取**对话框中，单击**确定**。 或者，如果在解决方案资源管理器中选择了一个解决方案或项目，则对于不希望检索的项，请清除其旁边显示的复选框。  
  
## <a name="see-also"></a>请参阅  
 [获取对话框&#40;源代码管理&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [设置和检索版本信息](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [查看项目历史记录](../../2014/database-engine/view-project-history.md)   
 [查看文件状态](../../2014/database-engine/view-file-status.md)  
  
  
