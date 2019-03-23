---
title: OData 源编辑器 （连接页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- Sql12.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 85ac46b918918f7e9dac715e11909ffeb9c46a29
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390458"
---
# <a name="odata-source-editor-connection-page"></a>OData 源编辑器（“连接”页）
  可以使用 **“OData 源编辑器”** 对话框的 **“连接”** 页，为 OData 源选择 OData 连接管理器。 通过此页还可以指定集合或资源路径和任何查询选项以指示需要从 OData 源检索的数据。 若要了解有关 OData 源的详细信息，请参阅 [OData Source](data-flow/odata-source.md)。  
  
## <a name="static-options"></a>静态选项  
 **OData 连接管理器**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
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
  
## <a name="see-also"></a>请参阅  
 [OData 源编辑器（“列”页）](../../2014/integration-services/odata-source-editor-columns-page.md)   
 [OData 源编辑器（“错误输出”页）](../../2014/integration-services/odata-source-editor-error-output-page.md)   
 [OData Connection Manager](connection-manager/odata-connection-manager.md)  
  
  
