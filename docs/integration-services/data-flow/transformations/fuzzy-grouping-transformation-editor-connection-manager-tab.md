---
title: "模糊分组转换编辑器 （连接管理器选项卡） |Microsoft 文档"
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
- sql13.dts.designer.fuzzygroupingtransformation.connection.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 47b1446d-5331-473c-9cb5-a98b1f55bf5f
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5bcb24248af5cc666ee45f53d60785fff679aca3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>模糊分组转换编辑器（“连接管理器”选项卡）
  使用 **“模糊分组转换编辑器”** 对话框的 **“连接管理器”** 选项卡可以选择现有连接或创建新的连接。  
  
> [!NOTE]  
>  连接指定的服务器必须正在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 模糊分组转换会在 tempdb 中创建临时数据对象，这些对象的大小可能与为此转换输入的所有内容完全一致。 在执行转换时，该转换将对这些临时对象发出服务器查询。 这会影响服务器的总体性能。  
  
 若要了解有关模糊分组转换的详细信息，请参阅 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
## <a name="options"></a>选项  
 **“无缓存”**  
 使用列表框选择现有的 OLE DB 连接管理器，或使用“新建”按钮创建新的连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建新的连接。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [通过使用模糊分组转换标识相似数据行](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
