---
title: 部署 JDBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2ab71ea3cdbe15993f1a1641ef9d5faed7f544d
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787804"
---
# <a name="deploying-the-jdbc-driver"></a>部署 JDBC 驱动程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  在部署依赖于 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的应用程序时，必须同时重新对 JDBC 驱动程序和此应用程序进行分配。 与 Windows 操作系统的组件 Windows 数据访问组件 (Windows DAC) 不同，JDBC 驱动程序被认为是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的组件。  
  
 有两种方法可用于部署 JDBC 驱动程序和应用程序。 一种方法是将 JDBC 驱动程序文件添加到您自己的自定义安装包中。 第二种方法涉及到使用 Microsoft 所提供的 JDBC 安装包，可以从 [Microsoft JDBC Driver for SQL Server 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=70166)下载此包。  
  
 以下各部分讨论如何在 Windows 和 UNIX 操作系统上使用 JDBC 安装包。  
  
> [!NOTE]  
>  有关部署 Java 应用程序的一般信息，请参阅 Java 网站。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>在 Windows 系统中部署 JDBC 驱动程序  
 在 Windows 操作系统上部署 JDBC 驱动程序时，必须使用安装包的可执行 zip 文件版本，其名称通常为 `sqljdbc_<version>_<language>.exe`。  
  
 若要无提示地运行可执行 zip 文件，必须在命令行上或批处理文件中使用 `/auto` 命令行选项，如下所示：  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  使用 `/auto` 选项时，执行的并不是真正的无提示安装，因为 WinZip 对话框仍会出现在用户屏幕上。 然而，您无需与其进行交互，解压缩操作完成后，它会立即关闭。  
  
## <a name="deploying-the-driver-on-unix-systems"></a>在 UNIX 系统中部署驱动程序  
 在 UNIX 操作系统上部署 JDBC 驱动程序时，必须使用安装包的 gzip 文件版本，其名称通常为 `sqljdbc_<version>_<language>.tar.gz`。  
  
 在安装 JDBC 驱动程序前，请确保用户的系统中安装了 gzip 和 tar 实用程序，并已将包含这两个实用程序可执行文件的文件夹添加到了 PATH 环境变量中。  
  
 若要解压缩此压缩的 tar 文件，请导航至您要解压缩驱动程序的目录中，然后键入以下命令：  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 若要解压缩此 tar 文件，请将它移到您要安装驱动程序的目录中，然后键入以下命令：  
  
 `tar –xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
