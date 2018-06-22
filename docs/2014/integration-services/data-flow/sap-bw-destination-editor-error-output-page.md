---
title: SAP BW 目标编辑器（“错误输出”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a543d811-0bd2-4890-a0d3-f5fdcd4524b8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 65e3a1254c03d76be77319cf2b1ff677e72f80c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015075"
---
# <a name="sap-bw-destination-editor-error-output-page"></a>SAP BW 目标编辑器（“错误输出”页）
  可以使用 **“SAP BW 目标编辑器”** 的 **“错误输出”** 页指定错误处理选项。  
  
 若要了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目标的详细信息，请参阅 [SAP BW 目标](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“错误输出”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“错误输出”** ，以打开编辑器的 **“错误输出”** 页。  
  
## <a name="options"></a>“常规”  
  
> [!NOTE]  
>  如果您不知道配置目标所需的所有值，可能需要询问您的 SAP 管理员。  
  
 **输入或输出**  
 查看输入的名称。  
  
 **列**  
 未使用此选项。  
  
 **错误**  
 指定发生错误时目标应执行的操作：忽略错误、重定向行或使组件失败。  
  
 **截断**  
 未使用此选项。  
  
 **Description**  
 查看操作的说明。  
  
 **将此值设置到选定的单元格**  
 指定发生错误或截断时目标应对所有选定单元格执行的操作：忽略错误、重定向行或使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="see-also"></a>请参阅  
 [SAP BW 目标编辑器&#40;连接管理器页&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 目标编辑器&#40;映射页&#41;](sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 目标编辑器（“高级”页）](sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  