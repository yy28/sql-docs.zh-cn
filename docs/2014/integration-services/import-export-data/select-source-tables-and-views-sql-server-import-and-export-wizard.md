---
title: 选择源表和视图（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6356cb594013d642741148dd85f7ddefc1e08ff0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436744"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>选择源表和源视图（SQL Server 导入和导出向导）
  使用 "**选择源表和视图**" 页可以指定要从数据源复制到目标的表和视图。  
  
> [!NOTE]  
>  如果选中了“表复制”选项，则不必复制表中的所有列。 选择目标表后，请单击 "编辑映射" 以显示 "**列映射**" 对话框。 **\<ignore>** 对于要跳过的列，请在 "**列映射**" 对话框的 "**目标**" 列中选择。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
  
### <a name="tables-and-views-list"></a>表和视图列表  
 **Source**  
 使用这些复选框，可以从可用表和视图的列表中进行选择，以复制到目标。 如果选择了源表或源视图并且不执行其他操作，将从源不加更改地复制架构和数据。  
  
 **目标**  
 从列表中为每个源表选择一个目标表。  
  
> [!NOTE]  
>  如果此时在向导中暂停操作，并使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他工具在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中创建目标表，新表不会立即出现在可用目标表的列表中。 若要刷新目标表的列表，请将两页返回到 "**选择目标**" 页，重新选择目标数据库，然后再次前进到 "**选择源表和视图**"。  
  
### <a name="other-options"></a>其他选项  
 **编辑映射**  
 使用 "**列映射**" 对话框可以指定要接收源数据的目标列。 您可以通过 \<ignore> 在 "**列映射**" 对话框的 "**目标**" 列中选择要跳过的列来只复制列的子集。  
  
 **预览**  
 在执行导入或导出之前，在 "**预览数据**" 对话框中预览源数据以对其进行验证。 "**预览数据**" 对话框最多可显示200行数据。  
  
 预览数据后，可能需要更改为数据源和目标选定的选项。 若要进行这些更改，请在 **“选择源表和源视图”** 页，单击 **“后退”** 返回到可以更改选项的上一页。  
  
  
