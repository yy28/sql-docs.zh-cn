---
title: 安装适用于 SQL Server 的 OLE DB 驱动程序 | Microsoft 文档
description: 安装和卸载 SQL Server 的 OLE DB 驱动程序
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
manager: jroth
ms.openlocfilehash: e779d51f535d3b3489c1fbe043c7ff9212b0e875
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800876"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>安装适用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

若要安装用于 SQL Server 的 OLE DB 驱动程序需要 msoledbsql.msi 安装程序。
运行安装程序并选择偏好的选项。 SQL Server 的 OLE DB 驱动程序可以是与早期版本的 Microsoft OLE DB 访问接口并行安装。

SQL Server 文件 （msoledbsql.dll，msoledbsqlr.rll），OLE DB 驱动程序安装在`%SYSTEMROOT%\system32\`。 此外，msoledbsql.msi 安装 32 位二进制文件中的 x64 `%SYSTEMROOT%\SysWOW64\`。

> [!NOTE]  
> OLE DB 驱动程序适用于 SQL Server 的所有相应的注册表设置都作为安装过程的一部分。  

SQL Server 标头和库文件 （msoledbsql.h 和 msoledbsql.lib），OLE DB 驱动程序安装在`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`。 此外，msoledbsql.msi 安装中的相同文件 x64 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`。  

通过 msoledbsql.msi，可以将 OLE DB 驱动程序分发适用于 SQL Server。 你可能需要在部署应用程序时安装用于 SQL Server 的 OLE DB 驱动程序。 安装多个包（对于用户而言就像是一次安装）的一种方法就是使用链接器和引导程序技术。 有关详细信息，请参阅[为 Visual Studio 2005 创作自定义引导程序包](https://go.microsoft.com/fwlink/?LinkId=115667)和[添加自定义系统必备](https://go.microsoft.com/fwlink/?LinkId=115668)。  
  
X64 msoledbsql.msi 还适用于 SQL Server 安装的 OLE DB 驱动程序的 32 位版本。 如果你的应用程序面向的平台不是其开发时，可以下载 msoledbsql.msi x64 和 x86 版本。

在调用 msoledbsql.msi 时，默认情况下仅安装客户端组件。 这些客户端组件即为那些支持运行使用适用于 SQL Server 安装的 OLE DB 驱动程序开发的应用程序的文件。 若还要安装 SDK 组件，请在命令行中指定 `ADDLOCAL=All`。 例如：  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>无提示安装  
 如果将 /passive、/qn、/qb 或 /qr 选项与 msiexec 一起使用，则必须还指定 IACCEPTMSOLEDBSQLLICENSETERMS=YES，以便显式指示接受最终用户许可协议条款。 必须以全大写字母指定此选项。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>为 SQL Server 的 OLE DB 驱动程序安装为依赖项  
一定不能卸载适用于 SQL Server OLE DB 驱动程序，直到依赖的所有应用程序都卸载它。 若要向用户提供应用程序依赖于 OLE DB 驱动程序适用于 SQL Server 的警告，使用 APPGUID 安装选项在 MSI 中，如下所示：  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

传递给 APPGUID 的值是您的特定产品代码。 当使用 Microsoft Installer 捆绑应用程序安装程序时，必须创建产品代码。
APPGUID 选项要求从提升的命令提示符运行安装程序。

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
