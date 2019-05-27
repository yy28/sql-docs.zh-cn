---
title: ADO NET 源编辑器 （连接管理器页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.connection.f1
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f3d9d2270603c3f38189478ccaaf48510085907f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061692"
---
# <a name="ado-net-source-editor-connection-manager-page"></a>ADO NET 源编辑器（“连接管理器”页）
  可以使用 **“ADO NET 源编辑器”** 对话框的 **“连接管理器”** 页，为源选择 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
 若要了解有关 ADO NET 源的详细信息，请参阅 [ADO NET Source](data-flow/ado-net-source.md)。  
  
 **打开“连接管理器”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开具有 ADO NET 源的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 ADO NET 源。  
  
3.  在 **“ADO NET 源编辑器”** 中，单击 **“连接管理器”**。  
  
## <a name="static-options"></a>静态选项  
 **ADO.NET 连接管理器**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 使用“配置 ADO.NET 连接管理器”对话框创建新的连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|Option|Description|  
|------------|-----------------|  
|表或视图|从 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 数据源中的表或视图中检索数据。|  
|SQL 命令|使用 SQL 查询从 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 数据源中检索数据。|  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 **预览版** 最多可以显示 200 行。  
  
> [!NOTE]  
>  预览数据时，数据类型为 CLR 用户定义类型的列不包含数据。 而是显示值“\<数值太大，无法显示>”或 System.Byte[]。 使用 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 访问接口访问数据源时，显示前一个值；使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 访问接口访问数据源时，显示后一个值。  
  
## <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **表或视图的名称**  
 从数据源的可用表列表或视图列表中选择表或视图的名称。  
  
### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **“浏览”**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
## <a name="see-also"></a>请参阅  
 [ADO NET 源编辑器（“列”页）](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [ADO NET 源编辑器（“错误输出”页）](../../2014/integration-services/ado-net-source-editor-error-output-page.md)   
 [ADO.NET 连接管理器](connection-manager/ado-net-connection-manager.md)  
  
  
