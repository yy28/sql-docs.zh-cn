---
title: 运行 Reporting Services 脚本文件 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8ad3c0bb7ea7700f457cfaa9e7cb08684624dc73
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571536"
---
# <a name="run-a-reporting-services-script-file"></a>运行 Reporting Services 脚本文件
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 脚本环境 (RS.exe) 从命令提示符处运行脚本文件。 RS.exe 有许多可供使用的命令提示符参数。 有关命令提示符选项的详细信息，请参阅 [RS.exe 实用工具 (SSRS)](../../reporting-services/tools/rs-exe-utility-ssrs.md)。 有关更多脚本示例，请参阅 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="sample-command-lines"></a>示例命令行  
  
-   在指定目标报表服务器的脚本环境中运行 Script.rss。 默认情况下会应用 Windows 身份验证：  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver  
    ```  
  
-   在指定用来对 Web 服务调用进行身份验证的用户名和密码的脚本环境中运行 Script.rss：  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   在将服务器超时值指定为 30 秒的脚本环境中运行 Script.rss：  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -l 30  
    ```  
  
-   在指定名为 *report*的全局脚本变量的脚本环境中运行 Script.rss。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -v report="Company Sales"  
    ```  
  
-   在指定以批处理方式运行脚本文件中的 Web 服务操作的脚本环境中运行 Script.rss。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [技术参考 (SSRS)](../../reporting-services/technical-reference-ssrs.md)  
  
  
