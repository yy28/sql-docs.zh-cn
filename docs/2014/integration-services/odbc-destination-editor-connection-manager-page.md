---
title: ODBC 目标编辑器 （连接管理器页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0c778d51d5fb8f8c0598fb8aefb747e41271c815
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060707"
---
# <a name="odbc-destination-editor-connection-manager-page"></a>ODBC 目标编辑器（“连接管理器”页）
  可以使用 **“ODBC 目标编辑器”** 对话框的 **“连接管理器”** 页，为目标选择 ODBC 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
 有关 ODBC 目标的详细信息，请参阅 [ODBC Destination](data-flow/odbc-destination.md)。  
  
 **打开“ODBC 目标编辑器”的“连接管理器”页**  
  
## <a name="task-list"></a>任务列表  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开包含 ODBC 目标的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 目标。  
  
-   在 **“ODBC 目标编辑器”** 中，单击 **“连接管理器”**。  
  
## <a name="options"></a>选项  
  
### <a name="connection-manager"></a>“ODBC 源编辑器”  
 从列表中选择现有 ODBC 连接管理器，或单击“新建”创建新的连接。 该连接可以指向支持 ODBC 的任何数据库。  
  
### <a name="new"></a>新版  
 单击 **“新建”**。 **“配置 ODBC 连接管理器编辑器”** 对话框随即打开，供您在其中创建新的连接管理器。  
  
### <a name="data-access-mode"></a>数据访问模式  
 选择将数据加载到目标的方法。 选项显示在下表中：  
  
|选项|Description|  
|------------|-----------------|  
|表名 - 批处理|选择此选项可将 ODBC 目标配置为在批处理模式下工作。 选择此选项后，以下选项可用：|  
||**表或视图的名称**：从列表中选择可用的表或视图。<br /><br /> 该列表仅包含前 1000 个表。 如果你的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (\*) 通配符输入名称的任何部分以便显示要使用的表。<br /><br /> **批大小**：键入用于大容量加载的批处理的大小。 这是作为一批加载的行数。|  
|表名 - 逐行|选择此选项可以将 ODBC 目标配置为一次一行将各行插入目标表中。 选择此选项后，以下选项可用：|  
||**表或视图的名称**：从列表中选择数据库中的可用表或视图。<br /><br /> 该列表仅包含前 1000 个表。 如果您的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (*) 通配符输入名称的任何部分以便显示要使用的表。|  
  
### <a name="preview"></a>预览  
 单击 **“预览”** 可以查看所选表的最多 200 行数据。  
  
## <a name="see-also"></a>请参阅  
 [ODBC 目标自定义属性](data-flow/odbc-destination-custom-properties.md)   
 [ODBC 目标编辑器（“映射”页）](../../2014/integration-services/odbc-destination-editor-mappings-page.md)   
 [ODBC 目标编辑器&#40;错误输出页&#41;](../../2014/integration-services/odbc-destination-editor-error-output-page.md)  
  
  
