---
title: "Document and Script an Analysis Services Database |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ba1f7a1a969b055261f5b32955b18ad83941e3c9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="document-and-script-an-analysis-services-database"></a>记录和编写 Analysis Services 数据库脚本
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]后[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署数据库，则可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]若要输出的元数据的数据库或数据库中包含的对象，作为 XML Analysis (XMLA) 编写脚本。 可以将该脚本输出到一个新的 **“XMLA 查询编辑器”** 窗口、文件或剪贴板。 有关 XMLA 的详细信息，请参阅 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)。  
  
 生成的 XMLA 脚本使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 元素定义脚本包含的对象。 如果生成了 CREATE 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Create** 命令和 ASSL 元素，它们可用于在实例上创建整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库结构。 如果生成了一个 ALTER 脚本，则所生成的 XMLA 脚本包含一个 XMLA **Alter** 命令和 ASSL 元素，它们可用于将现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的结构还原到创建脚本时数据库所处的状态。  
  
 可以通过多种方法使用从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库生成的 XMLA 脚本，其中包括：  
  
-   维护一个备份脚本，通过该脚本可以重新创建所有数据库对象和权限。  
  
-   创建或更新数据库开发代码。  
  
-   从现有的架构创建一个测试或开发环境。  
  
## <a name="see-also"></a>另请参阅  
 [修改或删除 Analysis Services 数据库](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [创建元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
