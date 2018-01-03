---
title: "在 Windows 2000 上配置 RDS |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc8126f454dcb5ac990f837fb04e667589658926
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="configuring-rds-on-windows-2000"></a>在 Windows 2000 上配置 RDS
如果你遇到困难获取 RDS 才能正常工作，为 Windows 2000 升级后，请按照下列步骤以解决此问题：  
  
1.  请确保 World Wide Web 发布服务通过导航到 http:// 服务器通过使用 Internet Explorer 运行第一个。 如果你不能访问这种方式中的 Web 服务器，打开命令提示符并输入以下命令，"NET 启动 W3SVC"。  
  
2.  在开始菜单中，选择运行。 键入 msdfmap.ini，然后单击确定以在记事本中打开 msdfmap.ini 文件。 检查 [连接默认] 部分中，并访问参数设置为 NOACCESS，如果将其更改为 READONLY。  
  
3.  使用 RegEdit 实用程序，导航到"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo"并确保**HandlerRequired**设置为 0 和**DefaultHandler**是""(Null 字符串)。  
  
     **请注意**如果到此节注册表进行任何更改，你必须停止并通过输入以下命令在命令提示符下重新启动 World Wide Web 发布服务:"NET 停止 W3SVC"和"NET 启动 W3SVC"。  
  
4.  使用 RegEdit 实用程序，在"HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"到注册表中导航并验证是否存在名为的项**提高**。 如果没有，则创建它。  
  
5.  使用 Internet 服务管理器，找到默认的网站，并查看 MSADC 虚拟根的属性。 检查目录安全/IP 地址和域名限制。 如果选中"访问被拒绝"，然后选择"授予"。  
  
 请务必尝试重新启动服务器，如果更改不会出现若要解决在第一个问题。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。从 Windows 8 和 Windows Server 2012 开始，RDS 服务器组件不再包含在 Windows 操作系统中。 将应用程序使用到 RDS 迁移[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)


