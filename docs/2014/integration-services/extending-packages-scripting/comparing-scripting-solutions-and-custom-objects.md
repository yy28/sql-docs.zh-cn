---
title: 比较脚本解决方案与自定义对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9529c7949d17b402f8c83d44417d8c4588f71e70
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368929"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>比较脚本解决方案与自定义对象
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 脚本任务或脚本组件可实现许多可用于自定义托管任务或数据流组件的相同功能。 下面是有助于您根据需要选择相应的任务类型的一些注意事项：  
  
-   如果配置或功能特定于单个包，则应使用脚本任务或脚本组件，而不是开发自定义对象。  
  
-   如果功能是一般功能，并可在将来供其他包和其他开发人员使用，则应创建自定义对象，而不是使用脚本解决方案。 您可以在任何包中使用自定义对象，而脚本只能在为其创建的包中使用。  
  
-   如果将在同一个包中重新使用代码，则应考虑创建一个自定义对象。 将一个脚本任务或组件的代码复制到另一个脚本任务或组件，将导致多个代码副本的维护和更新更加困难，从而降低可维护性。  
  
-   如果实现将随时间而发生变化，则可考虑使用自定义对象。 自定义对象的开发和部署可以独立于父包，而对脚本解决方案所做的更新则需要重新部署整个包。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [用自定义对象扩展包](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
