---
title: FTP 连接管理器编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP Connection Manager Editor
ms.assetid: 874b6585-255b-4a43-8396-bb08c3e8ac2b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6b363d622d82a2829e25e21bcf7d8cf21fe0962d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768181"
---
# <a name="ftp-connection-manager-editor"></a>FTP 连接管理器编辑器
  使用 **“FTP 连接管理器编辑器”** 对话框可以指定用于连接到 FTP 服务器的属性。  
  
> [!IMPORTANT]  
>  FTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 若要了解有关 FTP 连接管理器的详细信息，请参阅 [FTP Connection Manager](connection-manager/ftp-connection-manager.md)。  
  
## <a name="options"></a>选项  
 **服务器名称**  
 提供 FTP 服务器的名称。  
  
 **服务器端口**  
 指定用来连接的 FTP 服务器的端口号。 此属性的默认值为 **21**。  
  
 **用户名**  
 提供用于访问 FTP 服务器的用户名。 此属性的默认值为“匿名”。   
  
 **密码**  
 提供用于访问 FTP 服务器的密码。  
  
 **超时值(秒)**  
 指定任务超时之前经过的秒数。如果值为 **0** ，则表示不限制时间。 此属性的默认值为 **60**。  
  
 **使用被动模式**  
 指定是由服务器还是由客户端启动连接。 服务器使用主动模式启动连接，客户端使用被动模式启动连接。 此属性的默认值为“主动模式”。   
  
 **重试次数**  
 指定任务尝试连接的次数。 如果值为 **0** ，则表示不限制尝试次数。  
  
 **块区大小(KB)**  
 提供传输数据的块区大小 (KB)。  
  
 **测试连接**  
 在配置 FTP 连接管理器后，请通过单击“测试连接”确认该连接是否正常。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
