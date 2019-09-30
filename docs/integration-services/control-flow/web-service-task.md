---
title: Web 服务任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 343d3d0d16a19e6d7e1610eff84f6e1aa8ff860a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293802"
---
# <a name="web-service-task"></a>Web 服务任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Web 服务任务执行 Web 服务方法。 可以将 Web 服务任务用于下列目的：  
  
-   将 Web 服务方法返回的值写入变量。 例如，可以从 Web 服务方法获取某天的最高气温，然后使用此值更新设置列值的表达式中使用的变量。  
  
-   将 Web 服务方法返回的值写入文件。 例如，可以将潜在客户列表写入一个文件，然后将此文件用作在被写入数据库之前会清除数据的包中的数据源。  
  
## <a name="wsdl-file"></a>WSDL 文件  
 Web 服务任务使用 HTTP 连接管理器连接到 Web 服务。 HTTP 连接管理器与 Web 服务任务是单独配置的，在 Web 服务任务中要引用它。 HTTP 连接管理器指定服务器代理设置，如服务器 URL、访问 Web 服务服务器的凭据以及超时长度。 有关详细信息，请参阅 [HTTP 连接管理器](../../integration-services/connection-manager/http-connection-manager.md)。  
  
> [!IMPORTANT]  
>  HTTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 HTTP 连接管理器可以指向网站或 Web 服务描述语言 (WSDL) 文件。 指向 WSDL 文件的 HTTP 连接管理器的 URL 中包括 `?WSDL` 参数：例如， `https://MyServer/MyWebService/MyPage.asmx?WSDL`。  
  
 计算机本地必须有 WSDL 文件，以使用 **设计器提供的** “Web 服务任务编辑器” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对话框配置 Web 服务任务。  
  
-   如果 HTTP 连接管理器指向网站，则必须手动把 WSDL 文件复制到本地计算机。  
  
-   如果 HTTP 连接管理器指向 WSDL 文件，那么此文件可以由 Web 服务任务从网站下载到本地文件。  
  
 WSDL 文件列出 Web 服务提供的方法、方法要求的输入参数、方法返回的响应以及如何与 Web 服务通信。  
  
 如果方法使用输入参数，那么 Web 服务任务要求参数值。 例如，需要根据身高建议应该购买多长的滑雪板的 Web 服务方法，就要求在输入参数中提交您的身高。 该参数值可以通过任务中定义的字符串来提供，也可以通过任务作用域或父级容器中定义的变量来提供。 使用变量的优点在于可通过使用包配置或脚本来动态地更新参数值。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[包配置](../../integration-services/packages/package-configurations.md)。  
  
 许多 Web 服务方法不使用输入参数。 例如，获取本月出生的总统姓名的 Web 服务方法就不需要输入参数，因为该 Web 服务可以在本地确定本月。  
  
 Web 服务方法的结果可以写入变量或文件。 使用文件连接管理器可以指定文件，也可以提供将结果写入的变量名称。 有关详细信息，请参阅[文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)和 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)。  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Web 服务任务可用的自定义日志记录消息  
 下表列出了可以为 Web 服务任务启用的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|日志项|描述|  
|---------------|-----------------|  
|**WSTaskBegin**|任务已开始访问 Web 服务。|  
|**WSTaskEnd**|任务已完成 Web 服务方法。|  
|**WSTaskInfo**|有关任务的说明性信息。|  
  
## <a name="configuration-of-the-web-service-task"></a>Web 服务任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Web 服务任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击下列主题之一：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>Web 服务任务编辑器（“常规”页）
  使用“Web 服务任务编辑器”  对话框的“常规”  页，可以指定 HTTP 连接管理器，指定 Web 服务任务所使用的 Web 服务描述语言 (WSDL) 文件的位置，对 Web 服务任务进行说明，以及下载 WSDL 文件。  
  
### <a name="options"></a>选项  
 **HTTPConnection**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”，新建一个连接管理器  。  
  
> [!IMPORTANT]  
>  HTTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 **相关主题：** [HTTP 连接管理器](../../integration-services/connection-manager/http-connection-manager.md)、[HTTP 连接管理器编辑器（“服务器”页）](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 键入计算机本地上 WSDL 文件的完全限定路径，或单击浏览按钮 (…) 并定位到该文件  。  
  
 如果您已经将该 WSDL 文件手动下载到计算机，请选择此文件。 但是，如果尚未下载该 WSDL 文件，请执行以下步骤：  
  
-   创建文件扩展名为“.wsdl”的空文件。  
  
-   为 **WSDLFile** 选项选择此空文件。  
  
-   将 **OverwriteWSDLFile** 的值设置为 **True** ，以便用实际 WSDL 文件覆盖该空文件。  
  
-   单击 **“下载 WSDL”** 下载实际 WSDL 文件，并覆盖空文件。  
  
    > [!NOTE]  
    >  在“WSDLFile”  框中提供现有本地文件的名称后，才会启用“下载 WSDL”  选项。  
  
 **OverwriteWSDLFile**  
 指示是否可以覆盖 Web 服务任务的 WSDL 文件。  
  
 如果想使用 **“下载 WSDL”** 按钮下载 WSDL 文件，请将此值设置为 **True**。  
  
 **名称**  
 为 Web 服务任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入 Web 服务任务的说明。  
  
 **“下载 WSDL”**  
 下载 WSDL 文件。  
  
 当您在 **WSDLFile** 框中提供现有本地文件的名称后，该按钮才会启用。  
  
## <a name="web-service-task-editor-input-page"></a>Web 服务任务编辑器（“输入”页）
  可以使用 **“Web 服务任务编辑器”** 对话框的 **“输入”** 页，指定 Web 服务、Web 方法和作为输入提供给 Web 方法的值。 可通过直接在“值”列中键入字符串或在“值”列中选择变量来提供这些值。  
  
### <a name="options"></a>选项  
 **服务**  
 从列表中选择用来执行 Web 方法的 Web 服务。  
  
 **方法**  
 从列表中为要执行的任务选择 Web 方法。  
  
 **WebMethodDocumentation**  
 键入对 Web 方法的说明，或单击浏览按钮 (…)，再在“Web 方法文档”对话框中键入说明   。  
  
 **名称**  
 列出为 Web 方法提供的输入名称。  
  
 **类型**  
 列出输入的数据类型。  
  
> [!NOTE]  
>  Web 服务任务仅支持以下数据类型的参数：Primitive 类型（如 integer 和 string）、Primitive 类型的数组和序列，以及枚举。  
  
 **变量**  
 选中该复选框以使用变量来提供输入。  
  
 **ReplTest1**  
 如果选中了“变量”复选框，则请在列表中选择要提供输入的变量；否则，请键入要在输入中使用的值。  
  
## <a name="web-service-task-editor-output-page"></a>Web 服务任务编辑器（“输出”页）
  可以使用 **“Web 服务任务编辑器”** 对话框的 **“输出”** 页，指定 Web 方法返回的结果的存储位置。  
  
### <a name="static-options"></a>静态选项  
 **OutputType**  
 选择存储结果时所使用的存储类型。 此属性具有下表所列的选项。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**文件连接**|将结果存储在文件中。 选择此值将显示动态选项 **File**。|  
|**变量**|将结果存储在变量中。 选择此值将显示动态选项 **Variable**。|  
  
### <a name="outputtype-dynamic-options"></a>OutputType 动态选项  
  
#### <a name="outputtype--file-connection"></a>OutputType = 文件连接  
 **File**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”，新建一个连接管理器  。  
  
 **相关主题：** [文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>OutputType = 变量  
 **变量**  
 从列表中选择变量，或单击“\<新建变量...>”，创建新的变量  。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>相关内容  
 MSDN 库中的视频[操作说明：使用 Web 服务任务调用 Web 服务（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=259642)。  
