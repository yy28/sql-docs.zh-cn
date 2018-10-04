---
title: Excel 连接管理器编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 403fe52b67756a32a4229df83fdf9fa56a0bb8a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069487"
---
# <a name="excel-connection-manager-editor"></a>Excel 连接管理器编辑器
  使用 **“Excel 连接管理器编辑器”** 对话框可以将连接添加到现有或新的 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 工作簿文件。  
  
 若要了解有关 Excel 连接管理器的详细信息，请参阅 [Excel Connection Manager](connection-manager/excel-connection-manager.md)。  
  
> [!NOTE]  
>  无法连接到受密码保护的 Excel 文件。  
  
## <a name="options"></a>选项  
 **Excel 文件路径**  
 键入一个现有或新的 Excel 工作簿文件 (.xls) 的路径和文件名。  
  
> [!WARNING]  
>  **Excel 目标编辑器**自动创建该 Excel 文件，选择时**Excel 连接**指向新/不存在文件，然后单击**新建**为**Excel 工作表的名称**。  
  
 **“浏览”**  
 使用“打开”对话框可以导航到 Excel 文件所在的文件夹或要创建新文件的文件夹。  
  
 **Excel 版本**  
 指定用于创建文件的 Microsoft Excel 的版本。  
  
|选项|Description|  
|------------|-----------------|  
|Excel 97-2003|文件是使用 Excel 97 或更高版本创建的。|  
|Excel 3.0|文件是使用 Excel 3.0 创建的。|  
|Excel 4.0|文件是使用 Excel 4.0 创建的。|  
|Excel 5.0|文件是使用 Excel 95 (7.0) 创建的。|  
  
 **首行包含列名称**  
 指定所选工作表中的第一行数据是否包含列名称。 此选项的默认值为 **True**。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用 Foreach 循环容器循环遍历 Excel 文件和表](control-flow/foreach-loop-container.md)  
  
  
