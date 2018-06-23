---
title: 通过使用数据流路径编辑器设置路径属性 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 512249a4-83a6-4087-980d-a4344da48371
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f9b8b60299840327060bfc192ac4fced2773029f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026800"
---
# <a name="set-the-properties-of-a-path-by-using-the-data-flow-path-editor"></a>使用数据流路径编辑器设置路径属性
  路径连接两个数据流组件。 数据流必须包含至少两个已连接的数据流组件，才能设置路径属性。 有关详细信息，请参阅 [在数据流中添加或删除组件](data-flow/add-or-delete-a-component-in-a-data-flow.md) 和 [连接数据流中的组件](data-flow/connect-components-in-a-data-flow.md)。  
  
### <a name="to-set-path-properties"></a>设置路径属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击“数据流”选项卡，然后双击路径。  
  
4.  在 **“数据流路径编辑器”** 中，单击 **“常规”**。 然后，可以编辑默认的路径名称并提供路径说明。 还可以修改 PathAnnotation 属性。  
  
5.  单击“确定” 。  
  
6.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 路径](data-flow/integration-services-paths.md)   
 [数据流](data-flow/data-flow.md)  
  
  