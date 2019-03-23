---
title: 查找转换编辑器 （连接页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.referencetable.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f5c2971b1d4da669cadc57f0a557b32bf2b1adde
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389815"
---
# <a name="lookup-transformation-editor-connection-page"></a>查找转换编辑器（“连接”页）
  可以使用 **“查找转换编辑器”** 对话框的 **“连接”** 页选择连接管理器。 在选择 OLE DB 连接管理器时，会同时选择用来生成引用数据集的查询、表或视图。  
  
 若要了解有关查找转换的详细信息，请参阅 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 在 **“查找转换编辑器”** 对话框的“常规”页上选择 **“完全缓存”** 和 **“缓存连接管理器”** 时，下列选项可用：  
  
 **“完全缓存”**  
 从列表中选择现有的缓存连接管理器，或单击“新建”创建一个新连接。  
  
 **新建**  
 使用“缓存连接管理器编辑器”对话框创建新的连接。  
  
 在 **“查找转换编辑器”** 对话框的“常规”页上选择 **“完全缓存”**、 **“部分缓存”** 或 **“无缓存”** 以及 **“OLE DB 连接管理器”** 时，下列选项可用：  
  
 **“无缓存”**  
 从列表中选择现有的 OLE DB 连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建新的连接。  
  
 **使用表或视图**  
 从列表中选择现有表或视图，或单击“新建”创建新表。  
  
> [!NOTE]  
>  在此处选择的表名将由在 **“查找转换编辑器”** 的 **“高级”** 页上指定的 SQL 语句覆盖和替换。 有关详细信息，请参阅 [查找转换编辑器（“高级”页）](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)。  
  
 **新建**  
 通过使用“创建表”对话框创建一个新表。  
  
 **使用 SQL 查询的结果**  
 选择该选项后，可以通过浏览找到预先存在的查询、生成一个新查询、检查查询语法，然后预览查询结果。  
  
 **生成查询**  
 通过使用“查询生成器”可以创建要运行的 Transact-SQL 语句，查询生成器是一个用于通过浏览数据来创建查询的图形工具。  
  
 **“浏览”**  
 使用此选项可以找到保存为文件的预先存在的查询。  
  
 **分析查询**  
 检查查询的语法。  
  
 **预览**  
 使用“预览查询结果”对话框预览结果。 此选项最多可以显示 200 行。  
  
## <a name="external-resources"></a>外部资源  
 blogs.msdn.com 上的博客文章： [查找缓存模式](https://go.microsoft.com/fwlink/?LinkId=219518)  
  
## <a name="see-also"></a>请参阅  
 [查找转换编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [查找转换编辑器（“列”页）](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [查找转换编辑器（“高级”页）](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [查找转换编辑器（“错误输出”页）](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [模糊查找转换](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
