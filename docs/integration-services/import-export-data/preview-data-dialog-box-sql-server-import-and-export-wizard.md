---
title: “预览数据”对话框（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7750fc7d5ca5a45c38f8a4dba6a6c8f793564aac
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>“预览数据”对话框（SQL Server 导入和导出向导）
  指定要复制的数据后，可以选择单击“预览”  以打开“预览数据”  对话框。 在此页上，最多可以从数据源预览 200 行示例数据。 这会确认向导将复制你想要复制的数据。
  
## <a name="screen-shot-of-the-preview-data-page"></a>“预览数据”页的屏幕截图 
 下面的屏幕快照显示向导的“预览数据”  对话框。  
 
![导入和导出向导的“预览数据”页](../../integration-services/import-export-data/media/preview-data.png "Preview data page of the Import and Export Wizard")  
  
## <a name="preview-sample-data"></a>预览示例数据  
 **数据源**  
显示向导用于从数据源加载数据的查询。

如果选择了要复制的表格，则“源”字段会显示 `SELECT * FROM <table>` 查询，而不是表名称。 
  
 **示例数据网格**  
 显示查询从数据源返回的示例数据（最多 200 行）。  


## <a name="thats-not-right-i-want-to-change-something"></a>这不正确，我想要更改某些内容
预览数据后，你可能想更改之前在向导页面中选择的选项。 要进行这些更改，请单击“确定”，返回到“选择源表和视图”页，然后单击“后退”返回到前面可以更改选项的页面。

## <a name="whats-next"></a>下一步是什么？  
 预览要复制的数据并单击“确定” 后，“预览数据”  对话框将返回到“选择源表和源视图”  页或“配置平面文件目标”  页。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 或 [配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
