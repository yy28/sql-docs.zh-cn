---
title: 创建 InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9cd4a848-409f-4681-a390-1c49a2aadbd7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 056e541f6e1d297e086072dd01201fb670529056
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916377"
---
# <a name="create-infopackage"></a>创建 InfoPackage
  使用 **“创建 InfoPackage”** 对话框在 SAP Netweaver BW 系统中创建新的 InfoPackage。  
  
 从 **“SAP BW 目标编辑器”** 的 **“连接管理器”** 页可以打开 **“创建 InfoPackage”** 对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“创建 InfoPackage”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”  选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页中，找到 **“创建 SAP BW 对象”** 组框，选择 **“InfoPackage”** ，然后单击 **“创建”** 。  
  
## <a name="options"></a>选项  
 **InfoSource**  
 输入新 InfoPackage 应基于的 InfoSource 的名称。  
  
 **简短说明**  
 输入新 InfoPackage 的说明。  
  
 **源系统**  
 选择将与新 InfoPackage 相关联的源系统。  
  
 **属性**  
 指示 InfoPackage 将加载属性数据。  
  
 **文本**  
 指示 InfoPackage 将加载文本数据。  
  
 **事务**  
 指示 InfoPackage 将加载事务数据。  
  
 **保存并激活**  
 保存并激活该新 InfoPackage。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Connector 1.1 for SAP BW F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
