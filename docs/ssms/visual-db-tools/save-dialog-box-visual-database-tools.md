---
title: “保存”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdtsql.chm:65541
- vdt.dlgbox.save
ms.assetid: 2db60e24-79b5-4943-8891-f1684e16ce3d
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd0ba7a9430a37c8ef46ef6e3c7d03a617a4aea3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="save-dialog-box-visual-database-tools"></a>“保存”对话框 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
当您在表设计器中保存工作并且您的工作会影响其他表时，将显示此对话框。 使用此对话框可以确认将要保存的表。  
  
> [!NOTE]  
> 在保存表之前，您在表设计器中对表做出的更改并不会提交到数据库。 表一旦保存就无法撤消更改。 若要放弃未保存的更改，请关闭所有打开的表而不进行保存。  
  
## <a name="options"></a>“常规”  
**表受到影响时警告**  
指定下次保存所选的表时是否显示此对话框。 默认情况下，此框处于选中状态。 如果清除此选项，可以在“选项”对话框中重新选择该选项。  
  
**保存文本文件**  
显示“另存为”对话框，提示你指定用于保存列出受影响表的文本文件的位置。 此文件包含受您所做更改影响的表的列表。  
  
## <a name="see-also"></a>另请参阅  
[设计表 (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
