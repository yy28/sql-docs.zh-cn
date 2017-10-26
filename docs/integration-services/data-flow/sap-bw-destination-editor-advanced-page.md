---
title: "SAP BW 目标编辑器 （高级页） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwdestination.advanced.f1
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e15c7e770bc46c3ddc3a9f58ae99a5440617720d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-destination-editor-advanced-page"></a>SAP BW 目标编辑器（“高级”页）
  可以使用“SAP BW 目标编辑器”的“高级”页设置高级设置，如包大小和超时信息。  
  
 若要了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目标的详细信息，请参阅 [SAP BW 目标](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“高级”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”**中单击 **“高级”** ，以打开编辑器的 **“高级”** 页。  
  
## <a name="options"></a>选项  
  
> [!NOTE]  
>  如果您不知道配置目标所需的所有值，可能需要询问您的 SAP 管理员。  
  
 **包大小**  
 指定将同时传输的数据行数。 此参数的最佳值取决于 SAP Netweaver BW 系统和可能发生的额外数据处理。 通常，2000 到 20000 之间的值能提供最佳性能。  
  
 **触发进程链**  
 （可选）指定完成数据加载后要触发的进程链的名称。  
  
 **等待 InfoPackage 的超时时间**  
 指定目标应等待 InfoPackage 完成的最大秒数。  
  
 **等待数据传输完成**  
 指定目标是否应等待 SAP Netweaver BW 系统完成数据加载。  
  
 **不启动 InfoPackage (只等待)**  
 指定目标不触发 InfoPackage，而只是等待 SAP Netweaver BW 系统已开始加载数据的通知。  
  
## <a name="see-also"></a>另请参阅  
 [SAP BW 目标编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 目标编辑器 &#40;映射页 &#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 目标编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Microsoft Connector for SAP BW F1 帮助](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

