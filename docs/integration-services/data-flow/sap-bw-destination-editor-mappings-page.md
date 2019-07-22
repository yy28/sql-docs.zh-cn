---
title: SAP BW 目标编辑器（“映射”页）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7b935ea743d052c9efa15fb1598d4cec1818e7b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034177"
---
# <a name="sap-bw-destination-editor-mappings-page"></a>SAP BW 目标编辑器（“映射”页）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 **“SAP BW目标编辑器”** 的 **“映射”** 页将输入列映射到目标列。  
  
 若要了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目标的详细信息，请参阅 [SAP BW 目标](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“映射”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“映射”** ，以打开编辑器的 **“映射”** 页。  
  
## <a name="options"></a>选项  
  
> [!NOTE]  
>  如果您不知道配置目标所需的所有值，可能需要询问您的 SAP 管理员。  
  
 **“SAP BW 目标编辑器”** 的 **“映射”** 页包含两个部分：  
  
-   上面部分显示可用输入和目标列，您可以通过这个部分在这两类列之间创建映射。  
  
-   下面部分是一个表，其中列出哪些输入列已映射到哪些输出列。  
  
### <a name="upper-section-options"></a>上面部分的选项  
 上面部分有以下选项：  
  
 **可用输入列**  
 查看可用输入列的列表。  
  
 要将输入列映射到目标列，请将 **“可用输入列”** 列表中的列拖放到 **“可用目标列”** 列表中的列上。  
  
 **“可用目标列”**  
 查看可用目标列的列表。  
  
 要将输入列映射到目标列，请将 **“可用输入列”** 列表中的列拖放到 **“可用目标列”** 列表中的列上。  
  
 上面部分还有一个上下文菜单，您可以通过右键单击背景来打开。 此上下文菜单包含以下选项：  
  
-   **选择所有映射**  
  
-   **删除所选映射**  
  
-   **通过匹配名称映射项**  
  
### <a name="lower-section-columns"></a>下面部分的列  
 下面部分是一个映射表，其中包含以下列：  
  
 **输入列**  
 查看您所选的输入列。  
  
 要将不同输入列映射到相同目标列，请在该列表中选择不同输入列。 要删除映射，请选择“\<ignore>”以从输出中排除该输入列。  
  
 **目标列**  
 查看每个可用目标列，而不管是否已对该列进行映射。  
  
## <a name="see-also"></a>另请参阅  
 [SAP BW 目标编辑器（“连接管理器”页）](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 目标编辑器（“错误输出”页）](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [SAP BW 目标编辑器（“高级”页）](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW F1 帮助](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
