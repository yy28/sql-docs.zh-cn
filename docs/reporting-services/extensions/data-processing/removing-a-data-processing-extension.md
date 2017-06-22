---
title: "删除数据处理扩展插件 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e59120a2297617d9234dac070cb5c99b4d564d65
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="removing-a-data-processing-extension"></a>删除数据处理扩展插件
  若要删除数据处理扩展插件，只需删除**扩展**数据处理扩展配置文件中的元素。 如果你进行了报表服务器以及报表设计器的条目，请删除**扩展**从 RSReportServer.config 和 RSReportDesigner.config 文件的元素。 在删除配置信息之后，该数据处理扩展插件对于该组件将不再可用。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
