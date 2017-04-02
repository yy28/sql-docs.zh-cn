---
title: "查找转换编辑器（“高级”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.lookuptransformation.advanced.f1"
helpviewer_keywords: 
  - "查找转换编辑器"
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# 查找转换编辑器（“高级”页）
  可以使用 **“查找转换编辑器”** 对话框的 **“高级”** 页，配置部分缓存以及修改查找转换的 SQL 语句。  
  
 若要了解有关查找转换的详细信息，请参阅 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
## 选项  
 **缓存大小(32 位)**  
 调整 32 位计算机的缓存大小 (MB)。 默认值为 5 MB。  
  
 **缓存大小(64 位)**  
 调整 64 位计算机的缓存大小 (MB)。 默认值为 5 MB。  
  
 **为无匹配项的行启用缓存**  
 缓存在引用数据集内没有匹配项的行。  
  
 **缓存的分配额**  
 指定要针对在引用数据集内没有匹配项的行分配的缓存所占的百分比。  
  
 **修改 SQL 语句**  
 修改用来生成引用数据集的 SQL 语句。  
  
> [!NOTE]  
>  在此页上指定的可选 SQL 语句将覆盖并替换在 **“查找转换编辑器”** 的 **“高级”**页上指定的表名。 有关详细信息，请参阅[查找转换编辑器（“连接”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)。  
  
 **设置参数**  
 使用“设置查询参数”对话框将输入列映射到参数。  
  
## 外部资源  
 blogs.msdn.com 上的博客文章： [查找缓存模式](http://go.microsoft.com/fwlink/?LinkId=219518)  
  
## 另请参阅  
 [查找转换编辑器（“常规”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-general-page.md)   
 [查找转换编辑器（“连接”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [查找转换编辑器（“列”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [查找转换编辑器（“错误输出”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)   
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [模糊查找转换](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  