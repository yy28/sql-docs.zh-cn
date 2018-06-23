---
title: 查找进程链 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3b3792a55da4ee30d4e3c09a186ca1bf6d32c965
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123438"
---
# <a name="look-up-process-chain"></a>查找进程链
  使用 **“查找进程链”** 对话框查找在 SAP Netweaver BW 系统中定义的进程链。 当可用进程链列表显示时，选择您需要的进程链，然后源将使用需要的值填充关联的选项。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 源使用 **“查找进程链”** 对话框。 若要了解有关 SAP BW 源的详细信息，请参阅 [SAP BW Source](sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“查找进程链”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击“SAP BW 源”。  
  
3.  在 **“SAP BW 源编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“进程链”** 组框中，单击 **“查找”** 显示 **“查找进程链”** 对话框。  
  
     只有在“执行模式”为“P - 触发进程链”的情况下，“进程链”组框才会显示。  
  
## <a name="lookup-options"></a>查找选项  
 在查找字段中，您可以使用星号通配符 (*) 或使用部分字符串结合星号通配符来筛选结果。 但是，如果您将查找字段保留为空，则查找操作仅与该字段中的空字符串匹配。  
  
 **Process chain**  
 输入您要查找的进程链的名称，或输入部分名称加上星号通配符 (*)。 或者，仅使用星号通配符，以包括所有进程链。  
  
 **查找**  
 查找在 SAP Netweaver BW 系统中定义的匹配进程链。  
  
## <a name="lookup-results"></a>查找结果  
 单击“查找”按钮后，将在一个包含以下列标题的表中显示 SAP Netweaver BW 系统中进程链的列表。  
  
 **“进程链”**  
 显示在 SAP Netweaver BW 系统中定义的进程链的名称。  
  
 **Description**  
 显示进程链的说明。  
  
 当可用进程链列表显示时，选择您需要的进程链，然后源将使用需要的值填充关联的选项。  
  
## <a name="see-also"></a>请参阅  
 [SAP BW 源编辑器&#40;连接管理器页&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  