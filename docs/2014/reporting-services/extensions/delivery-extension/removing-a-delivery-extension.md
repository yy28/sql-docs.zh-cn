---
title: 删除传递扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5efe51d0c91a0321a17e539aeddbb26f0dc3a5fe
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036245"
---
# <a name="removing-a-delivery-extension"></a>删除传递扩展插件
  要删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件，只需从配置文件中删除传递扩展插件的 Extension 元素。 删除配置信息之后，传递扩展插件对于报表服务器将不再可用。  
  
 从配置文件中删除传递扩展插件的相应 Extension 元素后，它不再向报表服务器注册。 报表服务器从传递扩展插件的列表中删除此项，并停用使用该传递扩展插件的任何订阅。 当删除某个传递扩展插件后，用户不再能够选择它作为通知方法。  
  
## <a name="see-also"></a>请参阅  
 [实现传递扩展插件](implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
