---
title: 外部工具的参数 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2365ec137329675e2cd88e7f5bf7e1781aa3308f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52812409"
---
# <a name="arguments-for-external-tools"></a>外部工具的参数
  参数是在从“工具”菜单中启动外部工具时，由 Studio 环境提供值的变量。 可以使用“外部工具”对话框将外部工具（如记事本）添加到“工具”菜单。  
  
 下表列出了外部工具的参数。  
  
|“属性”|参数|Description|  
|----------|--------------|-----------------|  
|**项路径**|$(ItemPath)|当前源代码的完整文件名（以驱动器 + 路径 + 文件名形式定义）；如果一个非源代码窗口处于活动状态，则该参数将是空白的。|  
|**项目录**|$(ItemDir)|当前源代码的目录（以驱动器 + 路径形式定义）；如果一个非源代码窗口处于活动状态，则该参数将是空白的。|  
|**项文件名**|$(ItemFilename)|当前源代码的文件名（定义为文件名）；如果一个非源代码窗口处于活动状态，则该参数将是空白的。|  
|**项扩展名**|$(ItemExt)|当前源代码的文件扩展名|  
|**当前行** <sup>1</sup>|$(CurLine)|游标在编辑器中的当前行位置。|  
|**当前列**1|$(CurCol)|游标在编辑器中的当前列位置。|  
|**当前文本**1|$(CurText)|当前文本（当前游标位置下的字，或单行选择（如果存在））。|  
|**目标路径**|$(TargetPath)|目标的完整文件名（以驱动器 + 路径 + 文件名形式定义）。|  
|**目标目录**|$(TargetDir)|目标的目录。|  
|**目标名称**|$(TargetName)|目标的文件名。|  
|**目标扩展名**|$(TargetExt)|目标的文件扩展名。|  
|**项目目录**|$(ProjDir)|当前项目的目录（以驱动器 + 路径的形式定义）。|  
|**项目文件名**|$(ProjFileName)|当前项目的文件名（以驱动器 + 路径 + 文件名形式定义）。|  
|**解决方案目录**|$(SolutionDir)|当前解决方案的目录（以驱动器 + 路径的形式定义）。|  
|**解决方案文件名**|$(SolutionFileName)|当前解决方案的文件名（以驱动器 + 路径 + 文件名形式定义）。|  
  
 <sup>1</sup>当前行、 当前列中或当前文本基于游标在文本编辑器中的位置，在状态栏中所示。  
  
## <a name="see-also"></a>请参阅  
 [外部工具对话框](external-tools-dialog-box.md)   
 [常规用户界面元素](general-user-interface-elements.md)  
  
  
