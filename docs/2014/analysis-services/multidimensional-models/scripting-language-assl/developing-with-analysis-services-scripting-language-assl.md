---
title: 开发使用 Analysis Services 脚本语言 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfdce0d0db35d651d12670ffd3cb1c9437961cd1
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154273"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>使用 Analysis Services 脚本语言 (ASSL) 开发
  Analysis Services 脚本语言 (ASSL) 是对 XMLA 的扩展，该语言添加了对象定义语言和命令语言，用来在服务器上直接创建和管理 Analysis Services 结构。 您可以在自定义应用程序中使用 ASSL 通过 XMLA 协议与 Analysis Services 通信。 ASSL 由两个部分组成：  
  
-   数据定义语言 (DDL)（也称为对象定义语言）定义并说明 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例以及该实例所包含的数据库和数据库对象。  
  
-   向 Analysis Services 实例发送操作命令（如 `Create`、`Alter` 或 `Process`）的命令语言。 此命令语言述[XML for Analysis &#40;XMLA&#41;引用](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)。  
  
 若要查看描述 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 中的多维解决方案的 ASSL，可以在项目级别使用 View Code 命令。 您还可以在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中使用 XMLA 查询编辑器创建或编辑 ASSL 脚本。 生成的脚本可用于管理服务器上的对象或在服务器上运行命令。  
  
## <a name="see-also"></a>请参阅  
 [ASSL 对象和对象特征](assl-objects-and-object-characteristics.md)   
 [ASSL XML 约定](assl-xml-conventions.md)   
 [数据源和绑定（SSAS 多维）](../data-sources-and-bindings-ssas-multidimensional.md)  
  
  
