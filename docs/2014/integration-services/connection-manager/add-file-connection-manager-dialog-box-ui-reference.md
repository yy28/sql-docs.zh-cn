---
title: “添加文件连接管理器”对话框 UI 参考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileconnection.f1
helpviewer_keywords:
- Add File Connection Manager
ms.assetid: 9370bfb5-5993-4ad8-a9cd-2de53f320f34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 07c9f020fa3da424fa4524fb634ac33b84c993d4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784979"
---
# <a name="add-file-connection-manager-dialog-box-ui-reference"></a>“添加文件连接管理器”对话框 UI 参考
  可以使用 **“添加文件连接管理器”** 对话框定义与一组文件或文件夹的连接。  
  
 若要了解有关多文件连接管理器的详细信息，请参阅 [Multiple Files Connection Manager](multiple-files-connection-manager.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的内置任务和数据流组件不使用多文件连接管理器。 但是，可以在脚本任务或脚本组件中使用此连接管理器。  
  
## <a name="options"></a>选项  
 **使用类型**  
 指定要用于多个文件连接管理器的文件类型。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**创建文件**|连接管理器将创建文件。|  
|**现有文件**|连接管理器将使用现有文件。|  
|**创建文件夹**|连接管理器将创建文件夹。|  
|**现有文件夹**|连接管理器将使用现有文件夹。|  
  
 **文件/文件夹**  
 查看使用下面介绍的按钮所添加的文件或文件夹。  
  
 **“添加”**  
 通过使用“选择文件”对话框添加文件，或者通过使用“查找文件夹”对话框添加文件夹。  
  
 **编辑**  
 选择一个文件或文件夹，再通过使用“选择文件”或“查找文件夹”对话框，将其替换为另一个文件或文件夹。  
  
 **删除**  
 选择一个文件或文件夹，再通过使用“删除”按钮将其从列表中删除。  
  
 **箭头按钮**  
 选择一个文件或文件夹，再使用箭头按钮将它上移或下移以指定访问顺序。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../integration-services-error-and-message-reference.md)  
  
  
