---
title: 查看路径元数据在数据流路径编辑器 |Microsoft 文档
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
- metadata [Integration Services]
- paths [Integration Services], metadata
ms.assetid: 25cf8bdd-8691-4caa-96b6-3081b2f37dea
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4f775c2ee005b8f45f7a98c962ff1a8b6bb89649
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127109"
---
# <a name="view-path-metadata-in-the-data-flow-path-editor"></a>在数据流路径编辑器中查看路径元数据
  路径连接两个数据流组件。 若要查看路径元数据，数据流必须包含至少两个已连接的数据流组件。 有关详细信息，请参阅 [在数据流中添加或删除组件](data-flow/add-or-delete-a-component-in-a-data-flow.md) 和 [连接数据流中的组件](data-flow/connect-components-in-a-data-flow.md)。  
  
### <a name="to-view-path-metadata"></a>查看路径元数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击“数据流”选项卡，并双击路径。  
  
4.  在 **“数据流路径编辑器”** 对话框中，单击 **“元数据”**。  
  
5.  查看路径元数据，包括列名称、数据类型、精度、小数位、长度、代码页和每列源组件的名称。  
  
6.  若要复制元数据，请单击 **“复制到剪贴板”**。  
  
7.  单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 路径](data-flow/integration-services-paths.md)   
 [数据流](data-flow/data-flow.md)  
  
  