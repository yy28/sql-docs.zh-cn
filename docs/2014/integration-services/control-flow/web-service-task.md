---
title: Web 服务任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65c29338e713eab7650722b2b3801398379c0dac
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438034"
---
# <a name="web-service-task"></a>Web 服务任务
  Web 服务任务执行 Web 服务方法。 可以将 Web 服务任务用于下列目的：  
  
-   将 Web 服务方法返回的值写入变量。 例如，可以从 Web 服务方法获取某天的最高气温，然后使用此值更新设置列值的表达式中使用的变量。  
  
-   将 Web 服务方法返回的值写入文件。 例如，可以将潜在客户列表写入一个文件，然后将此文件用作在被写入数据库之前会清除数据的包中的数据源。  
  
## <a name="wsdl-file"></a>WSDL 文件  
 Web 服务任务使用 HTTP 连接管理器连接到 Web 服务。 HTTP 连接管理器与 Web 服务任务是单独配置的，在 Web 服务任务中要引用它。 HTTP 连接管理器指定服务器代理设置，如服务器 URL、访问 Web 服务服务器的凭据以及超时长度。 有关详细信息，请参阅 [HTTP 连接管理器](../connection-manager/http-connection-manager.md)。  
  
> [!IMPORTANT]  
>  HTTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 HTTP 连接管理器可以指向网站或 Web 服务描述语言 (WSDL) 文件。 指向 WSDL 文件的 HTTP 连接管理器的 URL 中包括 `?WSDL` 参数：例如， `http://MyServer/MyWebService/MyPage.asmx?WSDL`。  
  
 计算机本地必须有 WSDL 文件，以使用 **设计器提供的** “Web 服务任务编辑器” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对话框配置 Web 服务任务。  
  
-   如果 HTTP 连接管理器指向网站，则必须手动把 WSDL 文件复制到本地计算机。  
  
-   如果 HTTP 连接管理器指向 WSDL 文件，那么此文件可以由 Web 服务任务从网站下载到本地文件。  
  
 WSDL 文件列出 Web 服务提供的方法、方法要求的输入参数、方法返回的响应以及如何与 Web 服务通信。  
  
 如果方法使用输入参数，那么 Web 服务任务要求参数值。 例如，需要根据身高建议应该购买多长的滑雪板的 Web 服务方法，就要求在输入参数中提交您的身高。 该参数值可以通过任务中定义的字符串来提供，也可以通过任务作用域或父级容器中定义的变量来提供。 使用变量的优点在于可通过使用包配置或脚本来动态地更新参数值。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)和[包配置](../package-configurations.md)。  
  
 许多 Web 服务方法不使用输入参数。 例如，获取本月出生的总统姓名的 Web 服务方法就不需要输入参数，因为该 Web 服务可以在本地确定本月。  
  
 Web 服务方法的结果可以写入变量或文件。 使用文件连接管理器可以指定文件，也可以提供将结果写入的变量名称。 有关详细信息，请参阅[文件连接管理器](../connection-manager/file-connection-manager.md)和 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)。  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Web 服务任务可用的自定义日志记录消息  
 下表列出了可以为 Web 服务任务启用的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
|日志项|说明|  
|---------------|-----------------|  
|`WSTaskBegin`|任务已开始访问 Web 服务。|  
|`WSTaskEnd`|任务已完成 Web 服务方法。|  
|`WSTaskInfo`|有关任务的说明性信息。|  
  
## <a name="configuration-of-the-web-service-task"></a>Web 服务任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [Web 服务任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [Web 服务任务编辑器（“输入”页）](../web-service-task-editor-input-page.md)  
  
-   [Web 服务任务编辑器（“输出”页）](../web-service-task-editor-output-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Web 服务任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击下列主题之一：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>相关内容  
 technet.microsoft.com 上的视频 [如何：使用 Web 服务任务调用 Web 服务（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=259642)。  
  
 [如何通过 SSIS 包使用 Web 服务](https://www.c-sharpcorner.com/article/how-to-consume-web-service-through-ssis-package/)。  
  
  
