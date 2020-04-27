---
title: OLE DB 源编辑器（"连接管理器" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 22b7c9ea4012655043cac7eb7f3d432ef1e2e854
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057046"
---
# <a name="ole-db-source-editor-connection-manager-page"></a>OLE DB 源编辑器（“连接管理器”页）
  可以使用 **“OLE DB 源编辑器”** 对话框的 **“连接管理器”** 页，为源选择 OLE DB 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
> [!NOTE]  
>  若要从使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2007 的数据源加载数据，请使用 OLE DB 源。 使用 Excel 源无法从 Excel 2007 数据源加载数据。 有关详细信息，请参阅 [Configure OLE DB Connection Manager](configure-ole-db-connection-manager.md)。  
>   
>  若要从使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2003 或更低版本的数据源加载数据，请使用 Excel 源。 有关详细信息，请参阅 [Excel 源编辑器（“连接管理器”页）](../../2014/integration-services/excel-source-editor-connection-manager-page.md)。  
  
> [!NOTE]  
>  OLE DB `CommandTimeout`源的属性在**OLE DB 源编辑器**中不可用，但可以使用**高级编辑器**进行设置。 有关此属性的详细信息，请参阅 [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)的“Excel 源”部分。  
  
 若要了解有关 OLE DB 源的详细信息，请参阅 [OLE DB Source](data-flow/ole-db-source.md)。  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>打开“OLE 源编辑器”（“连接管理器”页）  
  
1.  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，向 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]包添加 OLE DB 源。  
  
2.  右键单击源组件，然后单击“编辑”。****  
  
3.  单击 **“连接管理器”**。  
  
## <a name="static-options"></a>静态选项  
 **OLE DB 连接管理器**  
 从列表中选择一个现有连接管理器，或通过单击“新建”**** 创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”**** 对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|选项|说明|  
|------------|-----------------|  
|表或视图|从 OLE DB 数据源中的表或视图中检索数据。|  
|表名变量或视图名变量|在变量中指定表或视图名称。<br /><br /> **相关信息：** [在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)|  
|SQL 命令|使用 SQL 查询从 OLE DB 数据源中检索数据。|  
|变量中的 SQL 命令|在变量中指定 SQL 查询文本。|  
  
 **预览**  
 通过使用“数据视图”**** 对话框预览结果。 **预览版** 最多可以显示 200 行。  
  
> [!NOTE]  
>  预览数据时，数据类型为 CLR 用户定义类型的列不包含数据。 而是显示值“\<数值太大，无法显示>”或 System.Byte[]。 使用 SQL OLE DB 访问接口访问数据源时，显示前一个值；使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 访问接口访问数据源时，显示后一个值。  
  
## <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **表或视图的名称**  
 从数据源的可用表列表或视图列表中选择表或视图的名称。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含表或视图名称的变量。  
  
### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”**** 来生成查询，或通过单击“浏览”**** 定位到包含查询文本的文件。  
  
 **Parameters**  
 如果已经在参数化查询文本中使用 ? 作为参数占位符输入了参数化查询，请使用 **“设置查询参数”** 对话框将查询输入参数映射到包变量。  
  
 **生成查询**  
 使用“查询生成器”**** 对话框可直观地构造 SQL 查询。  
  
 **浏览**  
 使用“打开”**** 对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
### <a name="data-access-mode--sql-command-from-variable"></a>数据访问模式 = 变量中的 SQL 命令  
 **变量名称**  
 选择包含 SQL 查询文本的变量。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [OLE DB 源编辑器 &#40;列 "页&#41;](../../2014/integration-services/ole-db-source-editor-columns-page.md)   
 [OLE DB 源编辑器 &#40;错误输出页&#41;](../../2014/integration-services/ole-db-source-editor-error-output-page.md)   
 [使用 OLE DB 源提取数据](data-flow/extract-data-by-using-the-ole-db-source.md)   
 [OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)  
  
  
