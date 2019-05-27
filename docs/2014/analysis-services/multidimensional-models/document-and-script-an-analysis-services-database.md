---
title: 记录和编写 Analysis Services 数据库脚本 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9284073781a91b21d588684b9071e6179a815613
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075119"
---
# <a name="document-and-script-an-analysis-services-database"></a>记录和编写 Analysis Services 数据库脚本
  在部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库后，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将数据库的元数据或数据库中包含的对象的元数据输出为 XML for Analysis (XMLA) 脚本。 可以将该脚本输出到一个新的 **“XMLA 查询编辑器”** 窗口、文件或剪贴板。 有关 XMLA 的详细信息，请参阅[Analysis Services 脚本语言&#40;ASSL&#41;引用](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)。  
  
 生成的 XMLA 脚本使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 元素定义脚本包含的对象。 如果生成了 CREATE 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Create** 命令和 ASSL 元素，它们可用于在实例上创建整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库结构。 如果生成了一个 ALTER 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Alter** 命令和 ASSL 元素，它们可用于将现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的结构还原到创建脚本时数据库所处的状态。  
  
 可以通过多种方法使用从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库生成的 XMLA 脚本，其中包括：  
  
-   维护一个备份脚本，通过该脚本可以重新创建所有数据库对象和权限。  
  
-   创建或更新数据库开发代码。  
  
-   从现有的架构创建一个测试或开发环境。  
  
## <a name="see-also"></a>请参阅  
 [修改或删除 Analysis Services 数据库](modify-or-delete-an-analysis-services-database.md)   
 [Alter 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Create 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
