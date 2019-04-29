---
title: 连接到 Sybase (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0805246d5b88138cfa97019d1e0cd524c82456c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061000"
---
# <a name="connect-to-sybase-sybasetosql"></a>连接到 Sybase (SybaseToSQL)
使用**连接到 Sybase**对话框以连接到你想要迁移的 Sybase Adaptive Server Enterprise (ASE) 实例。  
  
若要访问此对话框，请在**文件**菜单中，选择**连接到 Sybase**。 如果你之前已连接，则命令是**重新连接到 Sybase**。  
  
## <a name="options"></a>选项  
**提供程序**  
选择任何用于连接到 Sybase 服务器计算机上安装的提供程序。  
  
**模式**  
选择任一标准或高级连接模式。 在标准模式下，输入或选择的服务器名称、 端口、 用户名和密码值。 在高级模式下，提供了一个连接字符串。  
  
**服务器名称**  
输入或选择的名称或自适应的服务器的 IP 地址。 默认服务器名称是与计算机名称相同。 这是标准模式选项。  
  
**服务器端口**  
如果将非默认端口用于连接到 ASE，输入端口号。 默认端口号为 5000。 这是标准模式选项。  
  
**用户名**  
输入用于连接到 ASE 的用户名。 这是标准模式选项。  
  
**密码**  
输入用户名的密码。 这是标准模式选项。  
  
**连接字符串**  
输入连接到 ASE 的完整连接字符串。  
  
连接字符串包含参数名称和值对。 参数的名称因所使用的提供程序而异。  
  
**各种提供程序的连接参数如下所示：**  
  
1.  连接参数**OLE DB 访问接口**  
  
    |设置|Sybase 12.5 参数|Sybase 15 参数|  
    |-----------|-------------------------|-----------------------|  
    |服务器名称|服务器名称|“服务器”|  
    |端口|服务器端口地址|端口|  
    |“用户名”|用户 ID|用户 ID|  
    |Password|Password|Password|  
    |提供程序|提供程序|提供程序|  
  
    用于 Sybase ASE 12.5，一个连接字符串示例如下所示：  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    用于 Sybase ASE 月 15 日，一个连接字符串示例如下所示：  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  连接参数**ODBC 提供程序**  
  
    |设置|Sybase 12.5 月 15 日参数|  
    |-----------|-----------------------------|  
    |驱动程序名称|驱动程序|  
    |服务器名称|“服务器”|  
    |用户名|uid|  
    |Password|pwd|  
    |端口号|端口|  
  
    对于 Sybase ASE 12.5 或 15，一个连接字符串示例如下所示：  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  连接参数**ADO.NET 提供程序**  
  
    |设置|Sybase 12.5 月 15 日参数|  
    |-----------|-----------------------------|  
    |服务器名称|“服务器”|  
    |用户名|uid|  
    |Password|pwd|  
    |端口号|端口|  
  
    ADO.NET 提供程序的连接字符串的一个示例是以下操作：  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
有关详细信息，请参阅 ASE 文档。  
  
这是一个高级的模式选项。  
  
