---
title: 方法 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1bc758d7f59d9dbf82c7875c2d6c6c0a2b19f4c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="xml-elements---methods"></a>XML 元素的方法
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis (XMLA) 协议使用两种方法，**发现**和**执行**，提供应用程序访问的实例上的信息的标准方法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 由于这些方法是通过使用简单对象访问协议 (SOAP) 调用的，因此它们接受的输入和传递的输出都是 XML 格式。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可实现这两种方法，并与 XML for Analysis 1.1 规范兼容。  
  
## <a name="in-this-section"></a>本節內容  
 下面的主题介绍 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实现的 XMLA 方法。  
  
|方法|Description|  
|------------|-----------------|  
|[发现方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例检索信息，如可用数据库的列表或有关特定对象的详细信息。 使用检索的数据**发现**方法取决于传递给它的参数的值。|  
|[执行方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|将 XMLA 命令发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例。 这包括涉及数据传输的请求，如检索或更新服务器上的数据。|  
  
## <a name="see-also"></a>另请参阅  
 [XML 元素 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 数据类型 & #40;XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 元素 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
