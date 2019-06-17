---
title: 创建事务数据的 InfoCube | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 673cea01-a260-4fce-a1a0-f73839289805
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 167e799c873d586b06300a7e9433324391968d32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827931"
---
# <a name="create-infocube-for-transaction-data"></a>“创建事务数据的 InfoCube”
  使用 **“创建事务数据的 InfoCube”** 对话框为 SAP Netweaver BW 系统中的事务数据创建一个新的 InfoCube。  
  
 从 **“SAP BW 目标编辑器”** 的 **“连接管理器”** 页可以打开 **“创建事务数据的 InfoCube”** 对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“创建事务数据的 InfoCube”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”  选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页中，找到 **“创建 SAP BW 对象”** 分组框，选择 **“InfoCube”** ，然后单击 **“创建”** 。  
  
## <a name="general-options"></a>常规选项  
 **InfoCube 名称**  
 输入新 InfoCube 的名称。  
  
 **详细说明**  
 输入新 InfoCube 的说明。  
  
 **保存并激活**  
 保存并激活新的 InfoCube。  
  
## <a name="infocube-transfer-structure-options"></a>InfoCube 传输结构选项  
 InfoCube 传输结构部分可供您将数据流列与 InfoObject 关联。  
  
 **PipelineElement**  
 显示数据流输出中与 SAP BW 目标连接的列。  
  
 **PipelineDataType**  
 显示数据流列的数据类型。  
  
 **InfoObject**  
 显示与数据流列相关联的 InfoObject 的名称。  
  
 **“类型”**  
 显示与数据流列相关联的 InfoObject 的类型。 下表列出了该类型的可能值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|CHA|特征|  
|UNI|单位|  
|KYF|关键数字|  
|TIM|时间特征|  
  
 **Iobject - 搜索**  
 将现有的 InfoObject 与当前行的数据流列关联。 要进行此关联，请单击 **“搜索”** ，然后使用 **“查找 InfoObject”** 对话框选择现有的 InfoObject。 有关此对话框的详细信息，请参阅 [Look Up InfoObject](look-up-infoobject.md)。  
  
 选择现有的 InfoObject 后，组件会将选定的值填充在 **“InfoObject”** 和 **“类型”** 列中。  
  
 **Iobject - 新建**  
 创建一个新的 InfoObject 并将该新的 InfoObject 与当前行中的数据流列关联。 要创建新的 InfoObject，请单击 **“新建”** ，然后使用 **“新建 InfoObject”** 对话框创建 InfoObject。 有关此对话框的详细信息，请参阅 [Create New InfoObject](create-new-infoobject.md)。  
  
 创建新 InfoObject 后，组件会将新值填充在 **“InfoObject”** 和 **“类型”** 列中。  
  
 **Iobject - 删除**  
 删除 InfoObject 与当前行的数据流列之间的关联。 若要删除此关联，请单击 **“删除”** 。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
