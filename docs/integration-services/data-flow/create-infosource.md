---
title: 创建 InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3201c6a1d57486ec05e6f4076a78354a05a6306f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="create-infosource"></a>“创建 InfoSource”
  使用 **“创建 InfoSource”** 对话框创建一个新 InfoSource。 要创建新 InfoSource，请使用 **“创建事务数据的 InfoSource”** 或 **“创建主数据的 InfoSource”** 对话框。  
  
 从 **“SAP BW 目标编辑器”** 的 **“连接管理器”** 页可以打开 **“创建 InfoSource”**对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“创建 InfoSource”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”**中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页的 **“创建 SAP BW 对象”** 组框中，选择 **“InfoSource”**，然后单击 **“创建”**。  
  
## <a name="options"></a>“常规”  
 **事务数据**  
 创建事务数据的新 InfoSource。  
  
 如果您选择此选项，将打开 **“创建事务数据的 InfoSource”** 对话框。 您可使用 **“创建事务数据的 InfoSource”** 对话框来创建新的 InfoSource。 有关此对话框的详细信息，请参阅 [Create InfoSource for Transaction Data](../../integration-services/data-flow/create-infosource-for-transaction-data.md)。  
  
 **主数据**  
 创建主数据的新 InfoSource。  
  
 如果您选择此选项，将打开 **“创建主数据的 InfoSource”** 对话框。 您可使用 **“创建主数据的 InfoSource”** 对话框来创建新的 InfoSource。 有关此对话框的详细信息，请参阅 [Create InfoSource for Master Data](../../integration-services/data-flow/create-infosource-for-master-data.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Connector for SAP BW F1 帮助](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
