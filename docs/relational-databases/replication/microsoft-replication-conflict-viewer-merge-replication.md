---
title: "Microsoft 复制冲突查看器（合并复制）| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.replconflictviewer.cvmerge.f1
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: feff3e58f4069175fa2e12b617a40aa92043dcc2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="microsoft-replication-conflict-viewer-merge-replication"></a>Microsoft 复制冲突查看器（合并复制）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用复制冲突查看器，可以查看在复制同步过程中发生的所有冲突。 在两个不同的服务器上（例如，在发布服务器和订阅服务器上，或在两个不同的订阅服务器上）同时修改相同的数据时会发生冲突。 使用在创建时选择的冲突解决程序，复制可以自动解决冲突。 不过，使用复制冲突查看器可以在必要时选择不同的冲突解决方法。 可能会发生下列冲突：  
  
-   更新冲突。 在两个位置更改相同的数据时会发生更新冲突。 一个更改入选，而另一个更改落选。 您可以选择保留现有数据（入选数据），使用与现有数据冲突的数据（落选数据）来覆盖现有数据，或合并入选数据和落选数据并更新现有数据。  
  
-   插入冲突。 在一个位置插入行，当与其他位置所做的更改进行合并时，如果违反数据一致性规则，则会发生插入冲突。 您可以选择保留现有数据（入选数据），使用与现有数据冲突的数据（落选数据）来覆盖现有数据，或合并入选数据和落选数据并更新现有数据。  
  
-   删除冲突。 当在一个位置删除某行而在另一个位置更改同一行时，则会发生此冲突。  
  
 在同步过程中解决冲突后，落选行的数据将写入冲突表中。 无论是接受原始解决方法还是选择其他解决方法来解决冲突，都将从冲突表中删除记录的冲突行。 应定期检查冲突以减小冲突跟踪表的大小。  
  
> [!NOTE]  
>  包含逻辑记录的冲突不会显示在冲突查看器中。 若要查看有关这些冲突的信息，请使用复制存储过程。 有关详细信息，请参阅[查看合并发布的冲突信息（复制 Transact-SQL 编程）](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)。  
  
## <a name="options"></a>“常规”  
 复制冲突查看器划分为两个部分。 对话框的上半部分显示所选表的冲突列表。 单击冲突列表中的项时，将在对话框的下半部分显示该冲突的详细信息。  
  
 在对话框的下半部分会显示相关信息，描述发生冲突的原因（例如，在发布服务器和订阅服务器上更新了同一行）。 在下半部分中，冲突数据显示在两个相对应的列（**“冲突解决入选方”** 和 **“冲突解决落选方”**）中。 如果冲突发生在更新的数据和删除的数据之间，则对于冲突中删除的一方来说，可能没有可显示的数据。 在这种情况下，复制冲突查看器会在其中一列中显示一条消息，指示在一个位置删除了该行，在另一个位置更新了该行。 此外，它还会指出建议的解决方法。  
  
 不能在复制冲突查看器中编辑的数据（例如， **rowguid** 数据）以只读方式显示（方框带有阴影）。  
  
 **“数据库”**  
 选择包含具有冲突的发布的数据库。  
  
 **发布**  
 选择包含具有冲突的表的发布。  
  
 **表**  
 选择包含冲突的表。  
  
 **定义筛选器**  
 单击此项可打开 **“定义筛选器”** 对话框。  
  
 **应用或删除筛选器**  
 单击此项可应用或删除在 **“定义筛选器”** 对话框中定义的筛选器。  
  
 **全选**  
 单击此项可选择网格中列出的所有冲突。  
  
 **全部不选**  
 单击此项可取消选择网格中列出的所有冲突。  
  
 **删除**  
 单击此项可从查看器中删除所选冲突，并从复制系统表中删除与冲突关联的元数据。 等同于为所选的每个冲突单击“提交入选方”按钮（不对数据进行任何更改）。  
  
 **显示所有列**  
 选择此选项可显示表中的所有列。  
  
 **显示前五列以及包含冲突数据的其他列**  
 选择此选项可显示前五列以及所有包含冲突的列。 当表包含很多列，而您只想查看与解决冲突最相关的列时，这非常有用。 前五列始终包含在此视图中，因为标识行的字段（如主键或名称字段）通常位于表的前几列中。  
  
 **显示列信息** (**…**)  
 单击此项可查看列信息： **“表名”**、 **“列名”**、 **“数据类型”**和 **“列值”**。 除非值显示为只读，否则**“列值”** 是可编辑的。  
  
 **提交入选方**  
 单击此项可将冲突解决程序确定的行保留为入选方。 在单击此按钮之前，可以更改未显示为只读的任何列的值。  
  
 **提交落选方**  
 单击此项可将冲突解决程序确定的行接受为落选方。 在单击此按钮之前，可以更改未显示为只读的任何列的值。  
  
 **记录冲突详细信息**  
 选中此框可将冲突的详细信息记录到文件。 若要指定文件的位置，请指向 **“视图”** 菜单，再单击 **“选项”**。 输入一个值，或单击**“浏览(...)”**，然后导航到相应的文件。 单击 **“确定”** 可退出 **“选项”** 对话框。  
  
## <a name="see-also"></a>另请参阅  
 [查看和解决合并发布的数据冲突 (SQL Server Management Studio)](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
