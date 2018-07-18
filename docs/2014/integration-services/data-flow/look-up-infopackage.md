---
title: 查找 InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7c0cb7a4-cd07-44cc-85cb-eb1ad91f85fd
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce2da77e51370960d433981e28c32c5e7c4e55cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151318"
---
# <a name="look-up-infopackage"></a>查找 InfoPackage
  使用 **“查找 InfoPackage”** 对话框查找在 SAP Netweaver BW 系统中定义的 InfoPackage。 当 InfoPackage 列表显示时，选择您需要的 InfoPackage，然后目标将使用需要的值填充关联的选项。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目标使用 **“查找进程链”** 对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“查找 InfoPackage”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在“连接管理器”页面上的“InfoPackage/InfoSource”组框中，单击“查找”显示“查找 InfoPackage”对话框。  
  
## <a name="lookup-options"></a>查找选项  
 在查找字段中，您可以使用星号通配符 (*) 或使用部分字符串结合星号通配符来筛选结果。 但是，如果您将查找字段保留为空，则查找操作仅与该字段中的空字符串匹配。  
  
 **InfoPackage**  
 输入您要查找的 InfoPackage 的名称，或输入部分名称加上星号通配符 (*)。 或者，仅使用星号通配符，以包括所有 InfoPackage。  
  
 **InfoSource**  
 输入 InfoSource 的名称，或输入部分名称加上星号通配符 (*)。 或者，仅使用星号通配符以包括所有 InfoPackage（而无论 InfoSource 是什么）。  
  
 **源系统**  
 输入源系统的名称，或输入部分名称加上星号通配符 (*)。 或者，仅使用星号通配符以包括所有 InfoPackage（而无论源系统是什么）。  
  
 **查找**  
 查找在 SAP Netweaver BW 系统中定义的匹配 InfoPackage。  
  
## <a name="lookup-results"></a>查找结果  
 单击“查找”按钮后，将在一个包含以下列标题的表中显示 SAP Netweaver BW 系统中 InfoPackage 的列表。  
  
 **InfoPackage**  
 显示在 SAP Netweaver BW 系统中定义的 InfoPackage 的名称。  
  
 **类型**  
 显示 InfoPackage 的类型。 下表列出了该类型的可能值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|Trans.|事务数据。|  
|Attr.|属性数据。|  
|文本|文本。|  
  
 **Description**  
 显示 InfoPackage 的说明。  
  
 **InfoSource**  
 显示与 InfoPackage 相关联的 InfoSource（如果有）的名称。  
  
 **Source System**  
 显示源系统的名称。  
  
 当 InfoPackage 列表显示时，选择您需要的 InfoPackage，然后目标将使用需要的值填充关联的选项。  
  
## <a name="see-also"></a>请参阅  
 [SAP BW 目标编辑器&#40;连接管理器页&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
