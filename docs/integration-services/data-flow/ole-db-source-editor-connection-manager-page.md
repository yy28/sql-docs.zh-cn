---
title: "OLE DB 源编辑器 （连接管理器页） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f996b8e5fd5d361959a1c972718b730896a2d805
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="ole-db-source-editor-connection-manager-page"></a>OLE DB 源编辑器（“连接管理器”页）
  可以使用 **“OLE DB 源编辑器”** 对话框的 **“连接管理器”** 页，为源选择 OLE DB 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
> [!NOTE]  
>  若要从使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 的数据源加载数据，请使用 OLE DB 源。 使用 Excel 源无法从 Excel 2007 数据源加载数据。 有关详细信息，请参阅 [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)。  
>   
>  若要从使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 或更低版本的数据源加载数据，请使用 Excel 源。 有关详细信息，请参阅 [Excel 源编辑器（“连接管理器”页）](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md)。  
  
> [!NOTE]  
>  OLE DB 源的 **CommandTimeout** 属性未在 **“OLE DB 源编辑器”**中提供，但可以使用 **“高级编辑器”**进行设置。 有关此属性的详细信息，请参阅 [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)的“Excel 源”部分。  
  
 若要了解有关 OLE DB 源的详细信息，请参阅 [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)。  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>打开“OLE 源编辑器”（“连接管理器”页）  
  
1.  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，向 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]包添加 OLE DB 源。  
  
2.  右键单击源组件，然后单击“编辑”。  
  
3.  单击 **“连接管理器”**。  
  
## <a name="static-options"></a>静态选项  
 **“无缓存”**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|选项|Description|  
|------------|-----------------|  
|表或视图|从 OLE DB 数据源中的表或视图中检索数据。|  
|表名变量或视图名变量|在变量中指定表或视图名称。<br /><br /> **相关信息：** [在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 命令|使用 SQL 查询从 OLE DB 数据源中检索数据。|  
|变量中的 SQL 命令|在变量中指定 SQL 查询文本。|  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 **预览版** 最多可以显示 200 行。  
  
> [!NOTE]  
>  预览数据时，数据类型为 CLR 用户定义类型的列不包含数据。 改为值\<值太大，无法显示 > 或 System.Byte [] 显示。 使用 SQL OLE DB 访问接口访问数据源时，显示前一个值；使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口访问数据源时，显示后一个值。  
  
## <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **表或视图的名称**  
 从数据源的可用表列表或视图列表中选择表或视图的名称。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含表或视图名称的变量。  
  
### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
 **参数**  
 如果已经在参数化查询文本中使用 ? 作为参数占位符输入了参数化查询，请使用 **“设置查询参数”** 对话框将查询输入参数映射到包变量。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **浏览**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
### <a name="data-access-mode--sql-command-from-variable"></a>数据访问模式 = 变量中的 SQL 命令  
 **变量名称**  
 选择包含 SQL 查询文本的变量。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [OLE DB 源编辑器 &#40;列页 &#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)   
 [OLE DB 源编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)   
 [使用 OLE DB 源提取数据](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)   
 [OLE DB 连接管理器](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  
