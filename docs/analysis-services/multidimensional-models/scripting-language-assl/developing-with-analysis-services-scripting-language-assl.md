---
title: "开发使用 Analysis Services 脚本语言 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8ba45c74f873bc597dc9f5efc734259d9c98b6a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>使用 Analysis Services 脚本语言 (ASSL) 开发
  Analysis Services 脚本语言 (ASSL) 是对 XMLA 的扩展，该语言添加了对象定义语言和命令语言，用来在服务器上直接创建和管理 Analysis Services 结构。 您可以在自定义应用程序中使用 ASSL 通过 XMLA 协议与 Analysis Services 通信。 ASSL 由两个部分组成：  
  
-   数据定义语言 (DDL)（也称为对象定义语言）定义并说明 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例以及该实例所包含的数据库和数据库对象。  
  
-   如发送操作命令的命令语言**创建**， **Alter**，或**过程**，到的 Analysis Services 实例。 此命令语言述[XML for Analysis &#40;XMLA &#41;引用](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)。  
  
 若要查看描述 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 中的多维解决方案的 ASSL，可以在项目级别使用 View Code 命令。 您还可以在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中使用 XMLA 查询编辑器创建或编辑 ASSL 脚本。 生成的脚本可用于管理服务器上的对象或在服务器上运行命令。  
  
## <a name="see-also"></a>另请参阅  
 [ASSL 对象和对象特征](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [ASSL XML 约定](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
