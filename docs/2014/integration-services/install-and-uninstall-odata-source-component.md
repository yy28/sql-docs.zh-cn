---
title: 安装和卸载 OData 源组件 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ae48af3dec0be31d329548cbc0d7cd76007dacaf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016400"
---
# <a name="install-and-uninstall-odata-source-component"></a>安装和卸载 OData 源组件
  本主题提供有关在计算机上安装或删除 OData 源组件的说明。  
  
## <a name="installation"></a>安装  
 OData 源组件要求在计算机上安装以下必备组件。  
  
-   SQL Server Data Tools（用于设计包）  
  
-   SQL Server Integration Services（用于在 Visual Studio 外部运行包）  
  
 若要安装 OData 源组件，下载[SQL Server 2014 功能包](http://go.microsoft.com/fwlink/p/?LinkId=391999)然后运行以下 MSI 文件之一。  
  
-   用于 64 位平台的 ODataSourceForSQLServer2014-amd64.msi  
  
-   用于 32 位平台的 ODataSourceForSQLServer2014-x86.msi  
  
> [!IMPORTANT]  
>  64 位安装程序将同时安装 32 位和 64 位版本的 OData 源组件。 如果使用 32 位操作系统，则只需运行 32 位安装程序。  
  
## <a name="uninstallation"></a>卸载  
 可以从卸载 OData 源组件**程序和功能**菜单。 查找**Microsoft SQL Server SSIS OData 源组件 (x64)** 条目并单击**卸载**。  
  
  