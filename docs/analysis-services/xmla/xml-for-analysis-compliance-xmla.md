---
title: XML for Analysis 遵从性 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0c351f65ad644e3c33d352cb3cd9dbb71a03f242
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="xml-for-analysis-compliance-xmla"></a>XML for Analysis 遵从性 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis 1.1 规范描述了一种开放标准，该标准支持对位于万维网上的数据源的数据访问。 本主题详细介绍与支持的 XML for Analysis 1.1 规范的符合度[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
## <a name="compliant-items"></a>符合项  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 符合 XML for Analysis 1.1 规范中列出的所有必须遵循的内容。 此外，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还实现了 XML for Analysis 1.1 规范中描述的下列可选项。  
  
|项|规范|实现|  
|----------|-------------------|--------------------|  
|会话支持|在 XML for Analysis 1.1 规范的“Support for Statefulness in XML for Analysis”（XML for Analysis 中的有状态性支持）部分列出的 SOAP 标头元素。|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以规范所述方式，支持所有列出的 SOAP 标头元素。|  
  
## <a name="extensions"></a>扩展项  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还扩展了 XML for Analysis 1.1 规范，以支持下列附加特性和功能。  
  
|项|规范|实现|  
|----------|-------------------|--------------------|  
|协议协商|XML for Analysis 1.1 规范中不包含相关信息|通过添加 ProtocolCapabilities 标头元素[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以支持的协议功能协商。|  
|Discover 方法支持的 XML for Analysis (XMLA) 命令|XML for Analysis 1.1 规范支持下列命令：<br /><br /> [语句元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下列命令：<br /><br /> [Alter 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [备份元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [批处理元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [取消元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [创建元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [删除元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [删除元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [插入元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [锁定元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [撰写 MergePartitions 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [处理元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restore 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [语句元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Subscribe 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [同步元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [解除锁定元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [更新元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|表格行集中的列错误|未在 XML for Analysis 1.1 规范中列出。|[错误](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)元素由[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]列元素中包含的报告错误[行](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)元素。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis & #40;XMLA & #41;引用](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
