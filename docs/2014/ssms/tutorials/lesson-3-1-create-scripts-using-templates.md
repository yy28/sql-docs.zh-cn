---
title: 使用模板创建脚本| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8387cdaf85d6fd7750229fda86c8cb3122b61d90
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227067"
---
# <a name="create-scripts-using-templates"></a>使用模板创建脚本
  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了大量脚本模板，其中包含了许多常用任务的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 这些模板包含用户提供的值（如表名称）的参数。 使用该参数，可以只键入一次名称，然后自动将该名称复制到脚本中所有必要的位置。 可以编写自己的自定义模板，以支持频繁编写的脚本。 也可以重新组织模板树，移动模板或创建新文件夹以保存模板。 在以下练习中，将使用模板创建一个数据库，并指定排序规则模板。  
  
## <a name="using-templates"></a>使用模板  
  
#### <a name="to-create-a-script-using-a-template"></a>若要使用模板创建脚本，请执行以下操作：  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的“视图”  菜单上，单击“模板资源管理器” 。  
  
2.  模板资源管理器中的模板是分组列出的。 展开“数据库”，再双击“创建数据库”。  
  
3.  在“连接到数据库引擎”对话框中，填写连接信息，然后单击“连接”。 此时将打开一个新查询编辑器窗口，其中包含“创建数据库”模板的内容。  
  
4.  在 **“查询”** 菜单上，单击 **“指定模板参数的值”**。  
  
5.  在“指定模板参数的值”对话框中，“值”列包含一个 **Database_Name** 参数的建议值。 在“数据库名称”参数框中，键入 **Marketing**，然后单击“确定”。 请注意“Marketing”插入脚本中的几个位置。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建自定义模板](lesson-3-2-create-custom-templates.md)  
  
  
