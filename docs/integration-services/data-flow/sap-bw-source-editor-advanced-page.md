---
title: "SAP BW 源编辑器 （高级页） |Microsoft 文档"
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
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ac7757987c169f803f3b0adda7f27c94f090d7db
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-source-editor-advanced-page"></a>SAP BW 源编辑器（“高级”页）
  使用“SAP BW 源编辑器”的“高级”页指定字符串转换规则和超时时间，还可重置特定请求 ID 的状态。  
  
 若要了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 源组件的详细信息，请参阅 [SAP BW 源](../../integration-services/data-flow/sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
> [!IMPORTANT]  
>  从 SAP Netweaver BW 提取数据要求额外的 SAP 许可。 请向 SAP 核实以便确认这些要求。  
  
 **打开“连接管理器”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击“SAP BW 源”。  
  
3.  在 **“SAP BW 源编辑器”**中单击 **“高级”** ，以打开编辑器的 **“高级”** 页。  
  
## <a name="options"></a>选项  
  
> [!NOTE]  
>  如果您不知道配置源所需的所有值，可能需要询问您的 SAP 管理员。  
  
 **字符串转换**  
 指定要应用的字符串转换规则。  
  
|选项|Description|  
|------------|-----------------|  
|**自动字符串转换**|当 SAP Netweaver BW 系统为 Unicode 系统时，将所有字符串转换为 **nvarchar** 。 否则，将所有字符串转换为 **varchar**。|  
|**将字符串转换为 varchar**|将所有字符串转换为 **varchar**。|  
|**将字符串转换为 nvarchar**|将所有字符串转换为 **nvarchar**。|  
  
 **超时(秒)**  
 指定源应等待的最大秒数。  
  
> [!NOTE]  
>  只有在编辑器的“连接管理器”页中选中“W - 等待通知”作为“执行模式”的值时，此选项才有效。 有关详细信息，请参阅 [SAP BW 源编辑器（“连接管理器”页）](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)。  
  
 **请求 ID**  
 指定单击“重置”时要将哪个请求 ID 的状态重置为“G - Green”。  
  
 **重置**  
 在提示您进行确认后，可将指定请求 ID 的状态重置为“G - Green”。 当发生问题时，SAP Netweaver BW 系统将请求的状态标记为黄色或红色状态，此时此功能十分有用。  
  
## <a name="see-also"></a>另请参阅  
 [SAP BW 源编辑器（“连接管理器”页）](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 源编辑器 &#40;列页 &#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [SAP BW 源编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Microsoft Connector for SAP BW F1 帮助](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
