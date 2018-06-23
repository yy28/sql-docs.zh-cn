---
title: 由 Integration Services 服务记录的事件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f4a3b92a14785ed10c0e775f03a30cd6920ada2a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124122"
---
# <a name="events-logged-by-the-integration-services-service"></a>由 Integration Services 服务记录的事件
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务将各种消息记入 Windows 应用程序事件日志。 该服务会在服务启动时、服务停止时和特定问题出现时记录这些消息。  
  
 本主题提供有关该服务记入应用程序事件日志的常见事件消息的信息。 本主题中说明的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务记录的所有消息均以 SQLISService 为事件源。  
  
 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的常规信息，请参阅 [Integration Services 服务（SSIS 服务）](integration-services-service-ssis-service.md)。  
  
## <a name="messages-about-the-status-of-the-service"></a>有关服务状态的消息  
 当您选择安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 时，系统将安装并启动 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，且其启动类型将设置为自动。  
  
|事件 ID|符号名称|文本|说明|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|正在启动 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务。|服务即将启动。|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务已启动。|服务已启动。|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务启动失败。%n错误: %1|服务未能启动。 服务未能启动可能是由于安装已损坏或服务帐户不适当。|  
|258|DTS_MSG_SERVER_STOPPING|正在停止 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务。%n%n退出时停止所有正在运行的包: %1|服务正在停止，如果将服务配置为执行此操作，则所有正在运行的包都会停止。 可以在配置文件中设置 True 或 False 值来决定服务是否在自身停止时停止正在运行的包。 此事件的消息包括这项设置的值。|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务已停止。%n服务器版本 %1|服务已停止。|  
  
## <a name="messages-about-the-configuration-file"></a>有关配置文件的消息  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的设置存储在一个 XML 文件中，您可以修改该文件。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](../configuring-the-integration-services-service-ssis-service.md)。  
  
|事件 ID|符号名称|文本|说明|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务: %n指定配置文件的注册表设置不存在。 %n正尝试加载默认的配置文件。|包含配置文件路径的注册表项不存在或为空。|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务配置文件不存在。%n正在使用默认设置加载。|在指定位置不存在配置文件自身。|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务配置文件不正确。%n读取配置文件 %1 时出错%n%n正在使用默认设置加载服务器。|无法读取配置文件或配置文件无效。 此错误可能是由文件中的 XML 语法错误引起的。|  
  
## <a name="other-messages"></a>其他消息  
  
|事件 ID|符号名称|文本|说明|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务: 正在停止运行中的包。%n包实例 ID: %1%n包 ID: %2%n包名称: %3%n包说明: %4%n包|服务正在尝试停止运行中的包。 可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中监视和停止正在运行的包。 有关如何在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中管理包的信息，请参阅[包管理（SSIS 服务）](package-management-ssis-service.md)。|  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何查看日志项的信息，请参阅 [在“日志事件”窗口中查看日志项](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 包记录的事件](../performance/events-logged-by-an-integration-services-package.md)  
  
  