---
title: ODBC 源编辑器（"连接管理器" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.connection.f1
ms.assetid: e2c8dc83-6394-4d6c-9232-97e94be72431
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b0935ba4cd76a458bd26438556bab56e6cfa091c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424254"
---
# <a name="odbc-source-editor-connection-manager-page"></a>ODBC 源编辑器（“连接管理器”页）
  可以使用 **“ODBC 源编辑器”** 对话框的 **“连接管理器”** 页，为源选择 ODBC 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
 有关 ODBC 源的详细信息，请参阅 [ODBC Source](data-flow/odbc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“ODBC 源编辑器”的“连接管理器”页**  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开具有 ODBC 源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”**** 选项卡上，双击 ODBC 源。  
  
## <a name="options"></a>选项  
  
### <a name="connection-manager"></a>“ODBC 源编辑器”  
 从列表中选择现有 ODBC 连接管理器，或单击 **“新建”** 创建新的连接。 该连接可以指向支持 ODBC 的任何数据库。  
  
### <a name="new"></a>新建  
 单击 **“新建”**。 **“配置 ODBC 连接管理器编辑器”** 对话框随即打开，供您在其中创建新的 ODBC 连接管理器。  
  
### <a name="data-access-mode"></a>数据访问模式  
 选择从源选择数据的方法。 选项显示在下表中：  
  
|选项|说明|  
|------------|-----------------|  
|表名称|从 ODBC 数据源中的表或视图检索数据。 选择此选项后，请从列表中为以下选项选择一个值：|  
||**表或视图的名称**：从列表中选择一个可用表或视图，或键入正则表达式以标识该表。|  
||该列表仅包含前 1000 个表。 如果您的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (*) 通配符输入名称的任何部分以便显示要使用的表。|  
|SQL 命令|使用 SQL 查询从 ODBC 数据源中检索数据。 您应该采用正在使用的源数据库的语法编写查询。 选择此选项后，请采用以下方法之一输入查询：|  
||在 **“SQL 命令文本”** 字段中，输入 SQL 查询的文本。|  
||单击 **“浏览”** 从文本文件加载 SQL 查询。|  
||单击 **“分析查询”** 验证查询文本的语法。|  
  
### <a name="preview"></a>预览  
 单击 **“预览”** ，查看从选定的表或视图中提取的最多前 200 行数据。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 源自定义属性](data-flow/odbc-source-custom-properties.md)   
 [ODBC 源编辑器 &#40;列 "页&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)   
 [ODBC 源编辑器（“错误输出”页）](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
