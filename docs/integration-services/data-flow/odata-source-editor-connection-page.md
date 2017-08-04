---
title: "OData 源编辑器 （连接页） |Microsoft 文档"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6bb7a97ddbcae4868ee7b737358d4b30608e4df2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="odata-source-editor-connection-page"></a>OData 源编辑器（“连接”页）
  可以使用 **“OData 源编辑器”** 对话框的 **“连接”** 页，为 OData 源选择 OData 连接管理器。 通过此页还可以指定集合或资源路径和任何查询选项以指示需要从 OData 源检索的数据。 若要了解有关 OData 源的详细信息，请参阅 [OData Source](../../integration-services/data-flow/odata-source.md)。  
  
## <a name="static-options"></a>静态选项  
 **OData 连接管理器**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 选择或创建连接管理器以后，对话框会显示连接管理器所使用的 OData 协议版本。  
  
 **新建**  
 通过使用“OData 连接管理器编辑器”对话框创建新的连接管理器。  
  
 **使用集合或资源路径**  
 指定从源选择数据的方法。  
  
|选项|Description|  
|------------|-----------------|  
|集合|使用集合名称查询从 OData 源检索数据。|  
|资源路径|使用资源路径查询从 OData 源检索数据。|  
  
 **查询选项**  
 为查询指定选项。  例如：$top=5。  
  
 **馈送 url**  
 基于在此对话框中选择的选项显示只读馈送 URL。  
  
 **预览**  
 通过使用“预览”对话框预览结果。 **“预览”** 最多可以显示 20 行。  
  
## <a name="dynamic-options"></a>动态选项  
  
### <a name="use-collection-or-resource-path--collection"></a>使用集合或资源路径 = 集合  
 **集合**  
 从下拉列表中选择集合。  
  
### <a name="use-collection-or-resource-path--resource-path"></a>使用集合或资源路径 = 资源路径  
 **Resource path**  
 键入资源路径。 例如：Employees  
  
## <a name="see-also"></a>另请参阅  
 [OData 源编辑器 &#40;列页 &#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)   
 [OData 源编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)   
 [OData 连接管理器](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
