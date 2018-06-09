---
title: XML for Analysis (XMLA) 遵从性 |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b618fdd8cca3faed72afb0276f18cd928a3f31f7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576879"
---
# <a name="xml-for-analysis-xmla-compliance"></a>XML for Analysis (XMLA) 遵从性
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]  

  XML for Analysis 1.1 规范描述了一种开放标准，该标准支持对位于万维网上的数据源的数据访问。 本主题详细介绍与 XML for Analysis 1.1 规范支持的 Azure Analysis Services 和 SQL Server Analysis Services 的符合性的级别。  
  
## <a name="compliant-items"></a>符合项  
Analysis Services 符合 XML for Analysis 1.1 规范中列出的所有必需项。 此外，Analysis Services 实现 XML for Analysis 1.1 规范中所述的以下可选项。  
  
|项|规范|实现|  
|----------|-------------------|--------------------|  
|会话支持|在 XML for Analysis 1.1 规范的“Support for Statefulness in XML for Analysis”（XML for Analysis 中的有状态性支持）部分列出的 SOAP 标头元素。|Analysis Services，支持所有列出的 SOAP 标头元素规范中所述。|  
  
## <a name="extensions"></a>扩展项  
 Analysis Services 还将扩展 XML for Analysis 1.1 规范，支持下列附加功能和功能。  
  
|项|规范|实现|  
|----------|-------------------|--------------------|  
|协议协商|XML for Analysis 1.1 规范中不包含相关信息|添加 Analysis services 以支持的协议功能协商 ProtocolCapabilities 标头元素。|  
|Discover 方法支持的 XML for Analysis (XMLA) 命令|XML for Analysis 1.1 规范支持下列命令：<br /><br /> [语句元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Analysis Services 支持以下命令：<br /><br /> [Alter 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [备份元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [批处理元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [取消元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [创建元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [删除元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [删除元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [插入元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [锁定元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [撰写 MergePartitions 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [处理元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restore 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [语句元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Subscribe 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [同步元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [解除锁定元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [更新元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|表格行集中的列错误|未在 XML for Analysis 1.1 规范中列出。|[错误](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)元素用于 Analysis services 报告错误中包含的列元素[行](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)元素。|  
  
## <a name="see-also"></a>另请参阅
 [XML for Analysis (XMLA) 参考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
