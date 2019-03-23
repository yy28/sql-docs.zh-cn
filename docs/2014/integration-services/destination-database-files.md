---
title: 目标数据库文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4911084929f3ff69657a6d5e51c557f35929b45b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379915"
---
# <a name="destination-database-files"></a>目标数据库文件
  可以使用 **“目标数据库文件”** 对话框查看或更改目标服务器上的数据库文件的名称和位置，或为传输数据库任务指定网络文件位置。 有关此任务的详细信息，请参阅 [传输数据库任务](control-flow/transfer-database-task.md)。  
  
 若要使用源服务器上数据库文件的名称和位置自动填充此对话框，请首先在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中指定 **SourceConnection** 、 **SourceDatabaseName** 和 **SourceDatabaseFiles** 。  
  
## <a name="options"></a>选项  
 **目标文件**  
 目标服务器上作为传输目标的数据库文件的名称。  
  
 请输入文件名，或单击文件名以编辑该名称。  
  
 **目标文件夹**  
 数据库文件要传输到的目标服务器上的文件夹。  
  
 请输入文件夹路径，单击文件夹路径以编辑该路径，或单击“浏览”以找到数据库文件要传输到的目标服务器上的文件夹。  
  
 **网络文件共享**  
 数据库文件要传输到的目标服务器上的网络共享文件夹。 通过在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中为 **“方法”** 指定 **DatabaseOffline** 以脱机模式传输数据库时，可以使用 **“网络文件共享”** 。  
  
 请输入网络文件共享位置，或单击“浏览”以找到网络文件共享位置。  
  
 以脱机模式传输数据库时，数据库文件先复制到 **“网络文件共享”** 位置，然后才会传输到 **“目标文件夹”** 位置。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [传输数据库任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [传输数据库任务编辑器（“数据库”页）](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
