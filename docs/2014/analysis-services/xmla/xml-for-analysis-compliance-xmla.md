---
title: XML for Analysis 遵从性 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc7a8da77b72f25a68764636fbe15bc2d9e4ae04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267083"
---
# <a name="xml-for-analysis-compliance-xmla"></a>XML for Analysis 遵从性 (XMLA)
  XML for Analysis 1.1 规范描述了一种开放标准，该标准支持对位于万维网上的数据源的数据访问。 本主题详细介绍与 XML for Analysis 1.1 规范支持的符合性的级别[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
## <a name="compliant-items"></a>符合项  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 符合 XML for Analysis 1.1 规范中列出的所有必须遵循的内容。 此外，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还实现了 XML for Analysis 1.1 规范中描述的下列可选项。  
  
|项|规范|实现|  
|----------|-------------------|--------------------|  
|会话支持|在 XML for Analysis 1.1 规范的“Support for Statefulness in XML for Analysis”（XML for Analysis 中的有状态性支持）部分列出的 SOAP 标头元素。|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以规范所述方式，支持所有列出的 SOAP 标头元素。|  
  
## <a name="extensions"></a>扩展项  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还扩展了 XML for Analysis 1.1 规范，以支持下列附加特性和功能。  
  
|项|规范|实现|  
|----------|-------------------|--------------------|  
|协议协商|XML for Analysis 1.1 规范中不包含相关信息|[ProtocolCapabilities](xml-elements-headers/protocolcapabilities-element-xmla.md)由添加的标头元素[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以支持协议协商功能。|  
|Discover 方法支持的 XML for Analysis (XMLA) 命令|XML for Analysis 1.1 规范支持下列命令：<br /><br /> -   [Statement 元素&#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下列命令：<br /><br /> -   [Alter 元素&#40;XMLA&#41;](xml-elements-commands/alter-element-xmla.md)<br />-   [备份元素&#40;XMLA&#41;](xml-elements-commands/backup-element-xmla.md)<br />-   [批处理元素&#40;XMLA&#41;](xml-elements-commands/batch-element-xmla.md)<br />-   [BeginTransaction 元素&#40;XMLA&#41;](xml-elements-commands/begintransaction-element-xmla.md)<br />-   [Cancel 元素&#40;XMLA&#41;](xml-elements-commands/cancel-element-xmla.md)<br />-   [ClearCache 元素&#40;XMLA&#41;](xml-elements-commands/clearcache-element-xmla.md)<br />-   [CommitTransaction 元素&#40;XMLA&#41;](xml-elements-commands/committransaction-element-xmla.md)<br />-   [创建元素&#40;XMLA&#41;](xml-elements-commands/create-element-xmla.md)<br />-   [删除元素&#40;XMLA&#41;](xml-elements-commands/delete-element-xmla.md)<br />-   [DesignAggregations 元素&#40;XMLA&#41;](xml-elements-commands/designaggregations-element-xmla.md)<br />-   [Drop 元素&#40;XMLA&#41;](xml-elements-commands/drop-element-xmla.md)<br />-   [插入元素&#40;XMLA&#41;](xml-elements-commands/insert-element-xmla.md)<br />-   [锁定元素&#40;XMLA&#41;](xml-elements-commands/lock-element-xmla.md)<br />-   [MergePartitions 元素&#40;XMLA&#41;](xml-elements-commands/mergepartitions-element-xmla.md)<br />-   [NotifyTableChange 元素&#40;XMLA&#41;](xml-elements-commands/notifytablechange-element-xmla.md)<br />-   [处理元素&#40;XMLA&#41;](xml-elements-commands/process-element-xmla.md)<br />-   [Restore 元素&#40;XMLA&#41;](xml-elements-commands/restore-element-xmla.md)<br />-   [RollbackTransaction 元素&#40;XMLA&#41;](xml-elements-commands/rollbacktransaction-element-xmla.md)<br />-SetPasswordEncryptionKey 元素<br />-   [Statement 元素&#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)<br />-   [Subscribe 元素&#40;XMLA&#41;](xml-elements-commands/subscribe-element-xmla.md)<br />-   [Synchronize 元素&#40;XMLA&#41;](xml-elements-commands/synchronize-element-xmla.md)<br />-   [Unlock 元素&#40;XMLA&#41;](xml-elements-commands/unlock-element-xmla.md)<br />-   [Update 元素&#40;XMLA&#41;](xml-elements-commands/update-element-xmla.md)<br />-   [UpdateCells 元素&#40;XMLA&#41;](xml-elements-commands/updatecells-element-xmla.md)|  
|表格行集中的列错误|未在 XML for Analysis 1.1 规范中列出。|[错误](xml-elements-properties/error-element-xmla.md)所使用的元素[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]列中包含的元素的报告错误[行](xml-elements-properties/error-element-xmla.md)元素。|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis &#40;XMLA&#41;引用](xml-for-analysis-xmla-reference.md)  
  
  
