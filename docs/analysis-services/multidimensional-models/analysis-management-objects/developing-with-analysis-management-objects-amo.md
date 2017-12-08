---
title: "使用分析管理对象 (AMO) 进行开发 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- Analysis Management Objects, programming
- AMO, programming
ms.assetid: 91354fc9-22da-4724-b97f-3b1e7b0e69d3
caps.latest.revision: "47"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbcf54edc79a1e8254ad6210d327f4a83973f1fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="developing-with-analysis-management-objects-amo"></a>使用分析管理对象 (AMO) 进行开发
分析管理对象 (AMO) 是以编程方式访问的对象的完整库，使应用程序来管理正在运行的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。

本节介绍了 AMO 概念，着重于介绍主要对象、使用这些对象的方式和时间，以及它们之间的关联方式。 有关特定对象或类的详细信息，请参阅：

- [Microsoft.AnalysisServices Namespace](http://msdn.microsoft.com/library/microsoft.analysisservices.aspx)，有关参考文档
- [Analysis Services 管理对象 (AMO)](http://www.bing.com/search?q=Analysis+Services+Management+Objects+%28AMO%29)，作为 Bing.com 常规搜索。


 **SQL Server 2016 中的新增功能**

在 SQL Server 2016 中，AMO 将重构到多个程序集。 泛型类 （如服务器、 数据库和角色） 中**Microsoft.AnalysisServices.Core** Namespace。 特定于多维的 Api 仍会保留在[Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720.aspx)。

针对早期版本的 AMO 编写的应用程序和自定义脚本将继续不使用任何修改。 但是，如果你有脚本或应用程序面向 SQL Server 2016 具体而言，或需要重新生成自定义解决方案，请确保将新的程序集和命名空间添加到你的项目。

## <a name="see-also"></a>另请参阅
[使用 Analysis Services 脚本语言 &#40; 进行开发ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) 
[使用 Analysis Services 中的 XMLA 进行开发](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)
