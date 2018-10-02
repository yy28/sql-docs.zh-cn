---
title: “保存更改脚本”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 822dbca38dfa6cdf6934bec3353bba531c9e84e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804206"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>“保存更改脚本”对话框 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
此对话框可显示您在上次保存表以后所做更改的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 使用该对话框还可以将脚本保存到位于所选位置的文本文件中。  
  
当您在表设计器中对表进行的更改尚未保存时，则可访问此对话框。 在“表设计器”菜单上，单击“生成更改脚本”。  
  
> [!NOTE]  
> Visual Database Tools 提供的更改脚本没有包含错误处理功能。 这些脚本假设在工具打开后数据库对象没有发生更改，因此不会发生与更改相关的问题。 运行更改脚本之前，您应在脚本中包括适当的错误处理语句。  
  
## <a name="options"></a>选项  
**每次保存时自动生成更改脚本**  
如果选择此选项，则在每次保存对表的更改时都会显示“保存更改脚本”对话框。  
  
**是**  
打开“保存”对话框，在其中可选择保存文本文件的位置。  
  
**是**  
取消创建更改脚本。  
  
