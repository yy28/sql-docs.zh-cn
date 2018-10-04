---
title: 记录和编写 Analysis Services 数据库脚本 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 427b5278f743570162899c3e876a5e0505feb3ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124647"
---
# <a name="document-and-script-an-analysis-services-database"></a>记录和编写 Analysis Services 数据库脚本
  在部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库后，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将数据库的元数据或数据库中包含的对象的元数据输出为 XML for Analysis (XMLA) 脚本。 可以将该脚本输出到一个新的 **“XMLA 查询编辑器”** 窗口、文件或剪贴板。 有关 XMLA 的详细信息，请参阅[Analysis Services 脚本语言&#40;ASSL&#41;引用](../scripting/analysis-services-scripting-language-assl-for-xmla.md)。  
  
 生成的 XMLA 脚本使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 元素定义脚本包含的对象。 如果生成了 CREATE 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Create** 命令和 ASSL 元素，它们可用于在实例上创建整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库结构。 如果生成了一个 ALTER 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Alter** 命令和 ASSL 元素，它们可用于将现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的结构还原到创建脚本时数据库所处的状态。  
  
 可以通过多种方法使用从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库生成的 XMLA 脚本，其中包括：  
  
-   维护一个备份脚本，通过该脚本可以重新创建所有数据库对象和权限。  
  
-   创建或更新数据库开发代码。  
  
-   从现有的架构创建一个测试或开发环境。  
  
## <a name="see-also"></a>请参阅  
 [修改或删除 Analysis Services 数据库](modify-or-delete-an-analysis-services-database.md)   
 [Alter 元素&#40;XMLA&#41;](../xmla/xml-elements-commands/alter-element-xmla.md)   
 [创建元素&#40;XMLA&#41;](../xmla/xml-elements-commands/create-element-xmla.md)  
  
  
