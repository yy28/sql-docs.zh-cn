---
title: "记录和编写 Analysis Services 数据库脚本 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XML for Analysis, 脚本"
  - "XMLA, 脚本"
  - "脚本 [Analysis Services], 数据库"
  - "记录数据库"
  - "数据库 [Analysis Services], 记录"
  - "数据库 [Analysis Services], 脚本"
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# 记录和编写 Analysis Services 数据库脚本
  在部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库后，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将数据库的元数据或数据库中包含的对象的元数据输出为 XML for Analysis (XMLA) 脚本。 可以将该脚本输出到一个新的 **“XMLA 查询编辑器”** 窗口、文件或剪贴板。 有关 XMLA 的详细信息，请参阅 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)。  
  
 生成的 XMLA 脚本使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 元素定义脚本包含的对象。 如果生成了 CREATE 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Create** 命令和 ASSL 元素，它们可用于在实例上创建整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库结构。 如果生成了一个 ALTER 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Alter** 命令和 ASSL 元素，它们可用于将现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的结构还原到创建脚本时数据库所处的状态。  
  
 可以通过多种方法使用从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库生成的 XMLA 脚本，其中包括：  
  
-   维护一个备份脚本，通过该脚本可以重新创建所有数据库对象和权限。  
  
-   创建或更新数据库开发代码。  
  
-   从现有的架构创建一个测试或开发环境。  
  
## 另请参阅  
 [修改或删除 Analysis Services 数据库](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter 元素 (XMLA)](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Create 元素 (XMLA)](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  