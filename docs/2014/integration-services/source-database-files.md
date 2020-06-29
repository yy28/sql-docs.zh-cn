---
title: 源数据库文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.sourcedbfiles.f1
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 426f84123b84b7b2a7892f0143a4a64b44b680a2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421234"
---
# <a name="source-database-files"></a>源数据库文件
  可以使用 **“源数据库文件”** 对话框查看源服务器上的数据库文件的名称和位置，或者为传输数据库任务指定网络文件共享位置。 有关此任务的详细信息，请参阅 [传输数据库任务](control-flow/transfer-database-task.md)。  
  
 若要使用源服务器上数据库文件的名称和位置填充此对话框，请首先在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中指定 **SourceConnection** 和 **SourceDatabaseName** 。  
  
## <a name="options"></a>选项  
 **源文件**  
 源服务器上要传输的数据库文件的名称。 **“源文件”** 是只读的。  
  
 **源文件夹**  
 源服务器上包含要传输的数据库文件的文件夹。 **“源文件夹”** 是只读的。  
  
 **网络文件共享**  
 源服务器上要从中传输数据库文件的网络共享文件夹。 通过在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中为 **“方法”** 指定 **DatabaseOffline** 以脱机模式传输数据库时，可以使用 **“网络文件共享”** 。  
  
 输入网络文件共享位置，或单击浏览按钮 **（...）** 以找到网络文件共享位置。  
  
 以脱机模式传输数据库时，数据库文件在传输到目标服务器之前将被复制到源服务器上的 **“网络文件共享”** 位置。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [传输数据库任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [传输数据库任务编辑器（“数据库”页）](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
