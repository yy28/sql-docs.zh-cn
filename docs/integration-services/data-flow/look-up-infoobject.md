---
title: 查找 InfoObject | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6246042a70aca4edc07a36bc0dabe95be56c6d7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657967"
---
# <a name="look-up-infoobject"></a>查找 InfoObject
  使用 **“查找 InfoObject”** 对话框查找在 SAP Netweaver BW 系统中定义的 InfoObject。 当可用 InfoObject 列表显示时，选择您需要的 InfoObject，然后 SAP BW 目标将使用需要的值填充关联的选项。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目标使用 **“查找 InfoObject”** 对话框。 若要了解有关 SAP BW 目标的详细信息，请参阅 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“查找 InfoObject”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 目标。  
  
3.  在 **“SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页的 **“创建 SAP BW 对象”** 组框中，选择以下选项之一：  
  
    1.  选择 **“InfoCube”**。 然后单击 **“创建”**。 在 **“创建事务数据的 InfoCube”** 对话框中单击列表中某一行的 **“IObject”** 列中的 **“搜索”** 。 每一行表示包数据流中的一列。  
  
    2.  选择 **“InfoSource”**。 然后单击 **“创建”**。 在 **“创建 InfoSource”** 对话框中，选择 **“事务数据”**。 在 **“创建事务数据的 InfoSource”** 对话框中单击列表中某一行的 **“IObject”** 列中的 **“搜索”** 。 每一行表示包数据流中的一列。  
  
    3.  选择 **“InfoSource”**。 然后单击 **“创建”**。 在 **“创建 InfoSource”** 对话框中，选择 **“主数据”**。 在 **“创建主数据的 InfoSource”** 对话框中单击 **“查找”**。  
  
 您还可以单击 **“新建 InfoObject”** 对话框中 **“属性”** 部分中的 **“添加”** 来打开 **“查找 InfoObject”** 对话框。  
  
## <a name="lookup-options"></a>查找选项  
 在查找字段文本框中，您可以使用星号通配符 (*) 或使用部分字符串结合星号通配符来筛选结果。 但是，如果您将查找字段保留为空，则查找过程仅与该字段中的空字符串匹配。  
  
 **特征**  
 查找代表特征的 InfoObject。  
  
 **单位**  
 查找代表单位的 InfoObject。  
  
 **关键数字**  
 查找代表关键数字的 InfoObject。  
  
 **时间特征**  
 查找代表时间特征的 InfoObject。  
  
 **名称**  
 输入您要查找的 InfoObject 的名称，或输入部分名称加上星号通配符 (*)。 或者，仅使用星号通配符以包括所有 InfoObject。  
  
 **Description**  
 输入说明，或输入部分说明加上星号通配符 (*)。 或者，仅使用星号通配符以包括所有 InfoObject（而无论说明是什么）。  
  
 **查找**  
 查找在 SAP Netweaver BW 系统中定义的匹配 InfoObject。  
  
## <a name="lookup-results"></a>查找结果  
 单击“查找”按钮后，将在一个包含以下列标题的表中显示 SAP Netweaver BW 系统中 InfoObject 的列表。  
  
 **InfoObject**  
 显示在 SAP Netweaver BW 系统中定义的 InfoObject 的名称。  
  
 **文本(短)**  
 显示与 InfoObject 相关联的简短文本。  
  
 当可用 InfoObject 列表显示时，选择您需要的 InfoObject，然后目标将使用需要的值填充关联的选项。  
  
## <a name="see-also"></a>另请参阅  
 [“创建事务数据的 InfoCube”](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [“创建 InfoSource”](../../integration-services/data-flow/create-infosource.md)   
 [创建事务数据的 InfoSource](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [创建主数据的 InfoSource](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [新建 InfoObject](../../integration-services/data-flow/create-new-infoobject.md)   
 [SAP BW 目标编辑器（“连接管理器”页）](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 帮助](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
