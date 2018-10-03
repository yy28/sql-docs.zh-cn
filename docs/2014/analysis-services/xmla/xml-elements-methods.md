---
title: 方法 (XMLA) |Microsoft Docs
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
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1e073eae6637b726a473ea7bf95057ed1548982
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088587"
---
# <a name="methods-xmla"></a>方法 (XMLA)
  XML for Analysis (XMLA) 协议使用两种方法，`Discover`并`Execute`，以提供应用程序访问的实例上的信息的标准方法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 由于这些方法是通过使用简单对象访问协议 (SOAP) 调用的，因此它们接受的输入和传递的输出都是 XML 格式。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可实现这两种方法，并与 XML for Analysis 1.1 规范兼容。  
  
## <a name="in-this-section"></a>本节内容  
 下面的主题介绍 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实现的 XMLA 方法。  
  
|方法|Description|  
|------------|-----------------|  
|[发现方法&#40;XMLA&#41;](xml-elements-methods-discover.md)|从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例检索信息，如可用数据库的列表或有关特定对象的详细信息。 使用 `Discover` 方法检索到的数据取决于传递给该方法的参数的值。|  
|[执行方法&#40;XMLA&#41;](xml-elements-methods-execute.md)|将 XMLA 命令发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例。 这包括涉及数据传输的请求，如检索或更新服务器上的数据。|  
  
## <a name="see-also"></a>请参阅  
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 数据类型&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
