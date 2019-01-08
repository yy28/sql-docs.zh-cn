---
title: 替换模板参数 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1fa26c1bfec54e4e684bcd7e0967281a6ef3301
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769969"
---
# <a name="replace-template-parameters"></a>替换模板参数
  模板包含每次使用模板时可由实现特定值替换的参数。 在代码编辑器中打开模板之后，可以使用与您的实现相关的值替换这些参数。  
  
## <a name="before-you-begin"></a>开始之前  
 “指定模板参数的值”对话框是包含三列的网格。 “参数”和“类型”列是只读的，不能更改。 查看“值”列的内容，将任意默认值更改为对你的实现合适的值。  
  
 若要使用此对话框，必须将脚本中的参数按以下格式包括在尖括号 (`< >`) 中：`<`parameter_name`,` data_type `,`default_value`>`。  
  
## <a name="replace-template-parameters"></a>替换模板参数  
 在代码编辑器窗口中打开模板后：  
  
1.  在 **“查询”** 菜单上，单击 **“指定模板参数的值”**。  
  
2.  在“指定模板参数的值”对话框中，“值”列包含每个参数的建议值。 接受值或将其替换为新值。  
  
3.  单击“确定”关闭“替换模板参数”对话框并在查询编辑器中修改脚本。  
  
## <a name="see-also"></a>请参阅  
 [模板资源管理器](template-explorer.md)   
 [打开模板](open-a-template.md)  
  
  
