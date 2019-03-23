---
title: 创建 InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eba2d2d28c06a60cc8269a349996646726f59142
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379835"
---
# <a name="create-infosource"></a>“创建 InfoSource”
  使用 **“创建 InfoSource”** 对话框创建一个新 InfoSource。 要创建新 InfoSource，请使用 **“创建事务数据的 InfoSource”** 或 **“创建主数据的 InfoSource”** 对话框。  
  
 从 **“SAP BW 目标编辑器”** 的 **“连接管理器”** 页可以打开 **“创建 InfoSource”** 对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“创建 InfoSource”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页的 **“创建 SAP BW 对象”** 组框中，选择 **“InfoSource”**，然后单击 **“创建”**。  
  
## <a name="options"></a>选项  
 **事务数据**  
 创建事务数据的新 InfoSource。  
  
 如果您选择此选项，将打开 **“创建事务数据的 InfoSource”** 对话框。 您可使用 **“创建事务数据的 InfoSource”** 对话框来创建新的 InfoSource。 有关此对话框的详细信息，请参阅 [Create InfoSource for Transaction Data](create-infosource-for-transaction-data.md)。  
  
 **主数据**  
 创建主数据的新 InfoSource。  
  
 如果您选择此选项，将打开 **“创建主数据的 InfoSource”** 对话框。 您可使用 **“创建主数据的 InfoSource”** 对话框来创建新的 InfoSource。 有关此对话框的详细信息，请参阅 [Create InfoSource for Master Data](create-infosource-for-master-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
