---
title: “检测到数据库更改”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.schema.databasechangesdetected
- vdtsql.chm:65543
- vdtsql.chm:65554
ms.assetid: 91f13086-371f-46a2-9f46-804c1415f3ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6f1927d25ebbb5e93dc8ea94eb5ce4895ada000b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263883"
---
# <a name="database-changes-detected-dialog-box-visual-database-tools"></a>“检测到数据库更改”对话框 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果尝试保存数据库关系图或选定的表，但某些将受保存操作影响的数据库对象对于数据库已经过期，则会显示此对话框。 如果接受对话框中显示的更改，则将更新数据库以匹配关系图并改写其他用户所做的更改。  
  
> [!NOTE]  
> 虽然您无法撤消对表或数据库关系图所做的更改，但在保存表或关系图之前，这些更改并不会保存到数据库中。 通过选择“否”  并关闭所有打开的关系图而不进行保存，即可放弃所有未保存的更改。  
  
## <a name="options"></a>选项  
**检测到差异时警告**  
指定在您下次尝试保存数据库关系图或所选表时是否显示此对话框。 选中此项表示在您每次保存对于数据库已过期的关系图或表时，该对话框都仍会显示。 未选中此项表示该对话框不再显示。 默认情况下，此框处于选中状态。 如果取消选中此选项，可以在“选项”  对话框中重新选中它。  
  
**是**  
用列表中显示的所有更改更新数据库。  
  
**“否”**  
取消保存操作。  
  
> [!NOTE]  
> 若要刷新关系图以匹配数据库，请将其关闭而不保存更改，在服务器资源管理器中右键单击该关系图，再单击“刷新”，然后重新打开该关系图。  
  
**保存文本文件**  
显示“另存为”  对话框，用于为包含数据库更改列表的文本文件指定位置。  
  
## <a name="see-also"></a>另请参阅  
[协调数据库关系图与已修改的数据库 (Visual Database Tools)](../../ssms/visual-db-tools/reconcile-a-database-diagram-with-a-modified-database-visual-database-tools.md)  
[多用户环境 (Visual Database Tools)](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
