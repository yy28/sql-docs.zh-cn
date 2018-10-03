---
title: 删除传递扩展插件 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: daebad069ec1d9791ceab58af1d25f03524c82cc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704887"
---
# <a name="removing-a-delivery-extension"></a>删除传递扩展插件
  要删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件，只需从配置文件中删除传递扩展插件的 Extension 元素。 删除配置信息之后，传递扩展插件对于报表服务器将不再可用。  
  
 从配置文件中删除传递扩展插件的相应 Extension 元素后，它不再向报表服务器注册。 报表服务器从传递扩展插件的列表中删除此项，并停用使用该传递扩展插件的任何订阅。 当删除某个传递扩展插件后，用户不再能够选择它作为通知方法。  
  
## <a name="see-also"></a>另请参阅  
 [实现传递扩展插件](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
