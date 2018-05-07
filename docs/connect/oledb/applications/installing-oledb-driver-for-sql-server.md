---
title: 安装适用于 SQL Server OLE DB 驱动程序 |Microsoft 文档
description: 安装和卸载 SQL Server 的 OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0cbe9e82dac58e3ba4d15f4a608d914c73987af1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ole-db-driver-for-sql-server"></a>安装适用于 SQL Server OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

若要安装 SQL Server 的 OLE DB 驱动程序需要 msoledbsql.msi 安装程序。
运行安装程序，并使你首选的选择。 SQL Server 的 OLE DB 驱动程序可以使用的 Microsoft OLE DB 提供程序的早期版本并行安装。

SQL Server 文件 （msoledbsql.dll，msoledbsqlr.rll） OLE DB 驱动程序安装在`%SYSTEMROOT%\system32\`。 此外，msoledbsql.msi 安装中的 32 位二进制文件 x64 `%SYSTEMROOT%\SysWOW64\`。

> [!NOTE]  
> 有关 OLE DB 驱动程序的 SQL Server 的所有相应的注册表设置进行安装过程的一部分。  

SQL Server 标头和库文件 （msoledbsql.h 和 msoledbsql.lib） OLE DB 驱动程序安装在`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`。 此外，msoledbsql.msi 安装中的相同文件 x64 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`。  

你可以通过 msoledbsql.msi 适用于 SQL Server 分发 OLE DB 驱动程序。 你可能需要安装适用于 SQL Server 的 OLE DB 驱动程序，在部署应用程序时。 安装多个包（对于用户而言就像是一次安装）的一种方法就是使用链接器和引导程序技术。 有关详细信息，请参阅[为 Visual Studio 2005 创作自定义引导程序包](http://go.microsoft.com/fwlink/?LinkId=115667)和[添加自定义系统必备组件](http://go.microsoft.com/fwlink/?LinkId=115668)。  
  
X64 msoledbsql.msi 还会安装 OLE DB 驱动程序的 32 位版本 SQL Server。 如果你的应用程序面向的平台上开发以外的平台，你可以下载 msoledbsql.msi x64 和 x86 的版本。

在调用时 msoledbsql.msi，默认情况下安装仅客户端组件。 客户端组件是支持运行使用适用于 SQL Server 的 OLE DB 驱动程序开发的应用程序的文件。 若还要安装 SDK 组件，请在命令行中指定 `ADDLOCAL=All`。 例如：  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>无提示安装  
 如果你与 msiexec 一起使用以、 /qn、 /qb 或 /qr 选项，你还必须指定 IACCEPTMSOLEDBSQLLICENSETERMS = 是，以显式指示你接受最终用户许可协议的条款。 必须以全大写字母指定此选项。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>作为依赖项安装 for SQL Server 的 OLE DB 驱动程序  
很重要不会卸载所有的从属应用程序之前，为 SQL Server 上卸载 OLE DB 驱动程序。 若要为用户提供你的应用程序依赖于 OLE DB 驱动程序的 SQL Server 的警告，使用 APPGUID 安装选项中你 MSI，如下所示：  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

传递给 APPGUID 的值是您的特定产品代码。 当使用 Microsoft Installer 捆绑应用程序安装程序时，必须创建产品代码。
APPGUID 选项要求从提升的命令提示符运行安装程序。

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
