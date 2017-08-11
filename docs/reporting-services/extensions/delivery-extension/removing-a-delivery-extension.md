---
title: "删除传递扩展插件 |Microsoft 文档"
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
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e0d806bd57750b4e260ce0ba9fe48e86ac6d7386
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="removing-a-delivery-extension"></a>删除传递扩展插件
  若要删除[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]传递扩展插件，只需删除**扩展**你传递扩展插件配置文件中的元素。 删除配置信息之后，传递扩展插件对于报表服务器将不再可用。  
  
 一旦传递扩展插件的相应**扩展**从配置文件中删除元素，它不再向报表服务器注册。 报表服务器从传递扩展插件的列表中删除此项，并停用使用该传递扩展插件的任何订阅。 当删除某个传递扩展插件后，用户不再能够选择它作为通知方法。  
  
## <a name="see-also"></a>另请参阅  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
