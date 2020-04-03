---
title: 部署 JDBC 驱动程序
ms.custom: ''
ms.date: 03/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7e66360e08646a623aec5ed6f0b0f92d6ac62bf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "79433794"
---
# <a name="deploying-the-jdbc-driver"></a>部署 JDBC 驱动程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

在部署依赖于 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的应用程序时，必须同时重新对 JDBC 驱动程序和此应用程序进行分配。 与 Windows 操作系统的组件 Windows 数据访问组件 (Windows DAC) 不同，JDBC 驱动程序被认为是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的组件。  
  
有两种方法可用于部署 JDBC 驱动程序和应用程序。 一种方法是将 JDBC 驱动程序文件添加到您自己的自定义安装包中。 第二种方法涉及到使用 Microsoft 所提供的 JDBC 安装包，可以从 [Microsoft JDBC Driver for SQL Server 下载页](download-microsoft-jdbc-driver-for-sql-server.md)下载此包。  
  
以下各部分讨论如何在 Windows 和 UNIX 操作系统上使用 JDBC 安装包。  
  
> [!NOTE]  
> 有关部署 Java 应用程序的一般信息，请参阅 Java 网站。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>在 Windows 系统中部署 JDBC 驱动程序

在 Windows 操作系统上部署 JDBC 驱动程序时，必须解压已压缩的安装包，它的名称通常为 `sqljdbc_<version>_<language>.zip`。

## <a name="deploying-the-driver-on-unix-systems"></a>在 UNIX 系统中部署驱动程序

在 UNIX 操作系统上部署 JDBC 驱动程序时，必须使用安装包的 gzip 文件版本，其名称通常为 `sqljdbc_<version>_<language>.tar.gz`。  
  
在安装 JDBC 驱动程序前，请确保用户的系统中安装了 gzip 和 tar 实用程序，并已将包含这两个实用程序可执行文件的文件夹添加到了 PATH 环境变量中。  
  
若要解压缩此压缩的 tar 文件，请导航至您要解压缩驱动程序的目录中，然后键入以下命令：  
  
`gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
若要解压缩此 tar 文件，请将它移到您要安装驱动程序的目录中，然后键入以下命令：  
  
`tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>驱动程序重新分发的合法性

JDBC 驱动程序版本 6.0、6.2、6.4、7.0、7.2、7.4 和 8.2 是可再发行版本。 查看许可协议中的“可分发代码”子句  。

JDBC 驱动程序版本 4.x 是旧的过时版本。 对 4.x 的支持已在 2018 年之前过期。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
