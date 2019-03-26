---
title: 预览 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 551494c4-9e27-4592-9200-c6bf19e80c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cc444ff27f948ac452e6da05c6ba33113fb62f39
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289913"
---
# <a name="preview"></a>预览
  使用 **“预览”** 对话框可以预览 SAP BW 源所要提取的数据。  
  
> [!IMPORTANT]  
>  **“预览”** 选项位于 **“SAP BW 源编辑器”** 的 **“连接管理器”** 页，实际用来提取数据。 如果您已配置 SAP Netweaver BW 只提取自从上次提取后发生更改的数据，则选择 **“预览”** 将从下次数据提取中排除已经预览过的数据。  
  
 若要了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 源组件的详细信息，请参阅 [SAP BW 源](../../integration-services/data-flow/sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
> [!IMPORTANT]  
>  从 SAP Netweaver BW 提取数据要求额外的 SAP 许可。 请向 SAP 核实以便确认这些要求。  
  
 **打开“预览”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击“SAP BW 源”。  
  
3.  在 **“SAP BW 源编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  配置 SAP BW 源。  
  
5.  配置 SAP BW 源后，在 **“连接管理器”** 页中单击 **“预览”** ，在 **“预览”** 对话框中预览数据。  
  
    > [!NOTE]  
    >  单击 **“预览”** 还将打开 **“请求日志”** 对话框。 有关此对话框的详细信息，请参阅 [Request Log](../../integration-services/data-flow/request-log.md)。  
  
## <a name="options"></a>选项  
 **“预览”** 对话框显示从 SAP Netweaver BW 系统中请求的行。 显示的列为源数据中定义的列。  
  
 此对话框中没有其他选项。  
  
## <a name="see-also"></a>另请参阅  
 [SAP BW 源编辑器（“连接管理器”页）](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 帮助](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
