---
title: 请求日志 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 521d40529501d761b8e50300c16a816284109695
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770883"
---
# <a name="request-log"></a>请求日志
  使用 **“请求日志”** 对话框查看向 SAP Netweaver BW 系统提出样本数据请求的过程中记录的事件。 此信息可用于排除 SAP BW 源配置的故障。  
  
 若要了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 源组件的详细信息，请参阅 [SAP BW 源](sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
> [!IMPORTANT]  
>  从 SAP Netweaver BW 提取数据要求额外的 SAP 许可。 请向 SAP 核实以便确认这些要求。  
  
 **打开“请求日志”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”  选项卡上，双击“SAP BW 源”。  
  
3.  在 **“SAP BW 源编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  配置 SAP BW 源后，单击 **“预览”** ，预览 **“请求日志”** 对话框中的事件。  
  
    > [!NOTE]  
    >  单击 **“预览”** 还将打开 **“预览”** 对话框。 有关此对话框的详细信息，请参阅 [Preview](preview.md)。  
  
## <a name="options"></a>选项  
 **时间**  
 显示所记录事件的时间。  
  
 类型   
 显示所记录事件的类型。 下表列出了可能的事件类型。  
  
|值|说明|  
|-----------|-----------------|  
|S|成功消息。|  
|E|错误消息|  
|W|警告消息。|  
|I|信息性消息。|  
|A|操作已中止。|  
  
 **消息**  
 显示与记录事件相关联的消息文本。  
  
## <a name="see-also"></a>另请参阅  
 [SAP BW 源编辑器（“连接管理器”页）](sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
