---
title: "将防火墙配置为允许 FILESTREAM 访问 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbaaa631770966cff9cafa15fffb60b24dcd2767
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="configure-a-firewall-for-filestream-access"></a>将防火墙配置为进行 FILESTREAM 访问
  若要在防火墙保护的环境中使用 FILESTREAM，客户端和服务器都必须能够将 DNS 名称解析为包含 FILESTREAM 文件的服务器。 FILESTREAM 要求 Windows 文件共享端口 139 和 445 处于打开状态。  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>在运行 Windows 7 的计算机上打开 Windows 文件共享端口  
  
1.  在“控制面板”中，打开 **“Windows 防火墙”**。  
  
2.  在左窗格中，单击 **“高级设置”**。 如果系统提示您输入管理员密码或进行确认，请键入密码或提供确认。  
  
3.  在 **“高级安全 Windows 防火墙”** 对话框的左窗格中，单击 **“入站规则”**，然后在右窗格中单击 **“新建规则”**。  
  
4.  按照“新建入站规则”向导中的说明添加 TCP 端口 139。  
  
5.  重复上述步骤添加 TCP 端口 445。  
  
6.  关闭 **“高级安全 Windows 防火墙”** 对话框。  
  
  
