---
title: 对象 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, objects
ms.assetid: 768188ef-85d4-432a-9390-be05c835137f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e60cc807677b563361dbeea06c2f6b45ab468049
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149367"
---
# <a name="objects-xmla"></a>对象 (XMLA)
  XML for Analysis (XMLA) 协议使用两种方法，`Discover`并`Execute`，以提供应用程序访问的实例上的信息的标准方法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 由于这些方法是使用简单对象访问协议 (SOAP) 调用的，因此它们接受 XML 格式的输入并传送 XML 格式的输出。  
  
## <a name="in-this-section"></a>本节内容  
 下面的主题介绍 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 实现的 XMLA 对象。  
  
|方法|Description|  
|------------|-----------------|  
|[DiscoverResponse 元素&#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)|包含返回的实例的信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以响应[发现](xml-elements-methods-discover.md)方法调用。|  
|[ExecuteResponse 元素&#40;XMLA&#41;](xml-elements-objects-executeresponse.md)|包含返回的实例的信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以响应[Execute](xml-elements-methods-execute.md)方法调用。|  
  
## <a name="see-also"></a>请参阅  
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 数据类型&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
