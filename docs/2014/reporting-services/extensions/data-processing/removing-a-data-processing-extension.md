---
title: 删除数据处理扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 33
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0ea72edfcea9935b858631a639ec51f67a3feeac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126250"
---
# <a name="removing-a-data-processing-extension"></a>删除数据处理扩展插件
  要删除数据处理扩展插件，只需从配置文件中删除数据处理扩展插件的 Extension 元素。 如果为报表服务器以及报表设计器生成了条目，则从 RSReportServer.config 文件和 RSReportDesigner.config 文件中删除 Extension 元素。 在删除配置信息之后，该数据处理扩展插件对于该组件将不再可用。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 扩展插件](../reporting-services-extensions.md)   
 [实现数据处理扩展插件](implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  