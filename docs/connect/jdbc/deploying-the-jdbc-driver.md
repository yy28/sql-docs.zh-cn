---
title: "部署的 JDBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24e796670985c803b1a6f8a067ed6e8a548379e9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="deploying-the-jdbc-driver"></a>部署 JDBC 驱动程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  当部署的应用程序依赖于[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，必须与你的应用程序一起重新分发的 JDBC 驱动程序。 与 Windows 数据访问组件 (Windows DAC)，这是 Windows 操作系统的组成部分，不同的 JDBC 驱动程序被视为的一个组件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
 有两种方法可用于部署 JDBC 驱动程序和应用程序。 一种方法是将 JDBC 驱动程序文件添加到您自己的自定义安装包中。 第二种方法涉及使用 JDBC 安装包，你可以从下载的 Microsoft 提供的[Microsoft JDBC Driver for SQL Server 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=70166)。  
  
 以下各部分讨论如何在 Windows 和 UNIX 操作系统上使用 JDBC 安装包。  
  
> [!NOTE]  
>  有关部署 Java 应用程序的一般信息，请参阅 Java 网站。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>在 Windows 系统中部署 JDBC 驱动程序  
 在部署在 Windows 操作系统上的 JDBC 驱动程序时，你必须使用安装包，其中通常名为的可执行文件的 zip 文件版本`sqljdbc_<version>_<language>.exe`。  
  
 若要以静默方式运行可执行文件的 zip 文件，必须使用`/auto`命令行选项在命令行或批处理文件，如以下所示：  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  当你使用`/auto`它不是真正的无提示安装，WinZip 对话框中仍将显示在用户的屏幕上的选项。 然而，您无需与其进行交互，解压缩操作完成后，它会立即关闭。  
  
## <a name="deploying-the-driver-on-unix-systems"></a>在 UNIX 系统中部署驱动程序  
 在部署上 UNIX 操作系统的 JDBC 驱动程序时，你必须使用 gzip 文件版本的安装包，其中通常命名为`sqljdbc_<version>_<language>.tar.gz`。  
  
 在安装 JDBC 驱动程序前，请确保用户的系统中安装了 gzip 和 tar 实用程序，并已将包含这两个实用程序可执行文件的文件夹添加到了 PATH 环境变量中。  
  
 若要解压缩此压缩的 tar 文件，请导航至您要解压缩驱动程序的目录中，然后键入以下命令：  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 若要解压缩此 tar 文件，请将它移到您要安装驱动程序的目录中，然后键入以下命令：  
  
 `tar –xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

