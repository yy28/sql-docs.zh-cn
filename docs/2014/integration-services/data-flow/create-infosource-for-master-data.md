---
title: 创建主数据的 InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ea03885606cb47b1998d63c9aa2e98962709f27
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432284"
---
# <a name="create-infosource-for-master-data"></a>“创建主数据的 InfoSource”
  使用 **“创建主数据的 InfoSource”** 对话框为 SAP Netweaver BW 系统中的主数据创建一个新的 InfoSource。  
  
 从 **“SAP BW 目标编辑器”** 的 **“连接管理器”** 页可以打开 **“创建主数据的 InfoSource”** 对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“创建主数据的 InfoSource”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”  选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页的 **“创建 SAP BW 对象”** 组框中，选择 **“InfoSource”** ，然后单击 **“创建”** 。  
  
5.  在 **“创建 InfoSource”** 对话框中，选择 **“主数据”** ，然后单击 **“确定”** 。  
  
## <a name="options"></a>选项  
 **InfoObject 名称**  
 输入新 InfoSource 应基于的 InfoObject 的名称。  
  
 **查找**  
 查找 InfoObject。 此选项可打开 **“查找 InfoObject”** 对话框，您可从该对话框中选择 InfoObject。 有关此对话框的详细信息，请参阅 [Look Up InfoObject](look-up-infoobject.md)。  
  
 在您选择 InfoObject 后，组件会将选定 InfoObject 的名称填充在 **“InfoObject 名称”** 文本框中。  
  
 **新建**  
 新建 InfoObject。 此选项可打开“新建 InfoObject”对话框，您可在其中创建新的 InfoObject  。 有关此对话框的详细信息，请参阅 [Create New InfoObject](create-new-infoobject.md)。  
  
 创建 InfoObject 后，组件会将新 InfoObject 的名称填充在 **“InfoObject 名称”** 文本框中。  
  
 **简短说明**  
 输入新 InfoSource 的简短说明。  
  
 **详细说明**  
 输入新 InfoSource 的详细说明。  
  
 **源系统**  
 选择要与新 InfoSource 相关联的源系统。  
  
 **应用程序**  
 输入要与新 InfoSource 关联的应用程序的名称。  
  
 **属性**  
 指示主数据由属性组成。  
  
 **文本**  
 指示主数据由属性组成。  
  
 **保存并激活**  
 保存并激活该新 InfoSource。  
  
## <a name="see-also"></a>另请参阅  
 [“创建 InfoSource”](create-infosource.md)   
 [Microsoft Connector 1.1 for SAP BW F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
