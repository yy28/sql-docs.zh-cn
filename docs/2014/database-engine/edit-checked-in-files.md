---
title: 编辑签入文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97d6ab997a1ece36919a49243e0f1dc3cc6f3593
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779601"
---
# <a name="edit-checked-in-files"></a>编辑签入文件
  通常，必须先将源代码管理的文件签出，才能对其进行编辑。 不过，您可以对[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]进行配置，以便修改未签出的文件。执行此操作时，所做的更改将保留在内存中，直到你保存文件。 然后会提示您从源代码管理中签出文件。  
  
 如果您在小组中工作，除非您的源代码管理提供程序同时支持本地版本和服务器版本签出，否则不推荐您使用允许编辑签入文件的功能。 大多数提供程序都不支持本地版本签出。 如果您的提供程序不支持本地版本签出并且您需要编辑签入文件，则必须手动合并内存中版本和服务器版本，才能签入文件。 在此情况下，不支持自动合并和由提供程序辅助的合并。  
  
### <a name="to-edit-checked-in-files"></a>编辑签入的文件  
  
1.  在“工具” **** 菜单上，单击“选项” ****。  
  
2.  在 "**选项**" 对话框中，展开 "**源源代码**" 文件夹，然后单击 "**环境**"。  
  
3.  单击 "**允许编辑签入的项**"，然后单击 **"确定"**。  
  
## <a name="see-also"></a>另请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  
