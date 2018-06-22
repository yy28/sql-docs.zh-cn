---
title: 编辑签入文件 |Microsoft 文档
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
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd91efe4bd802a64ced4e6f93ac65f16ed4e5a71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014885"
---
# <a name="edit-checked-in-files"></a>编辑签入文件
  通常，必须先将源代码管理的文件签出，才能对其进行编辑。 但是，可以配置 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，以便修改尚未签出的文件。执行此操作时，更改将暂存在内存中，直到保存文件为止。 然后会提示您从源代码管理中签出文件。  
  
 如果您在小组中工作，除非您的源代码管理提供程序同时支持本地版本和服务器版本签出，否则不推荐您使用允许编辑签入文件的功能。 大多数提供程序都不支持本地版本签出。 如果您的提供程序不支持本地版本签出并且您需要编辑签入文件，则必须手动合并内存中版本和服务器版本，才能签入文件。 在此情况下，不支持自动合并和由提供程序辅助的合并。  
  
### <a name="to-edit-checked-in-files"></a>若要编辑签入文件  
  
1.  在“工具”  菜单上，单击“选项” 。  
  
2.  在**选项**对话框框中，展开**源 Contro**l 文件夹，然后单击**环境**。  
  
3.  单击**允许签入的项以编辑**，然后单击**确定**。  
  
## <a name="see-also"></a>请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  