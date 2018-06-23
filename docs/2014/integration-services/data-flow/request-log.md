---
title: 请求日志 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f37c7c97863eac901830c7efff3925ab25364688
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126590"
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
  
2.  在“数据流”选项卡上，双击“SAP BW 源”。  
  
3.  在 **“SAP BW 源编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  配置 SAP BW 源后，单击 **“预览”** ，预览 **“请求日志”** 对话框中的事件。  
  
    > [!NOTE]  
    >  单击 **“预览”** 还将打开 **“预览”** 对话框。 有关此对话框的详细信息，请参阅 [Preview](preview.md)。  
  
## <a name="options"></a>“常规”  
 **Time**  
 显示所记录事件的时间。  
  
 **类型**  
 显示所记录事件的类型。 下表列出了可能的事件类型。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|S|成功消息。|  
|E|错误消息|  
|W|警告消息。|  
|I|信息性消息。|  
|仅当辅助副本配置为使用手动故障转移模式，并且至少一个辅助副本当前与主要副本同步时，|操作已中止。|  
  
 **Message**  
 显示与记录事件相关联的消息文本。  
  
## <a name="see-also"></a>请参阅  
 [SAP BW 源编辑器&#40;连接管理器页&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  