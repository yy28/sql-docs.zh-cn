---
title: "发行说明 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 44c73c4d632fd434fcd296dc6fc2cc70af26086c
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes"></a>发行说明
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Windows 上的 Microsoft ODBC Driver for SQL Server 发行说明。  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新增内容[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上

**添加功能**:

BCP api 始终加密支持

新的连接字符串属性 UseFMTOnly 会导致在特殊情况下需要临时表使用旧的元数据的驱动程序。

Azure SQL 托管实例 （扩展特邀预览阶段） 的支持。 
> [!NOTE]
> 在使用托管实例时，有一些差异：
> -   不支持 FILESTREAM 
> -   本地文件系统访问是不受支持，但需要 tracefiles 之类的内容 
> -   从本地创建 UDT 不支持路径 
> -   不支持 Windows 集成身份验证 
> -   不支持 DTC 
> -   'sa' 帐户不存在 （默认帐户称为 cloudSA）
> -   TDS 令牌错误 (0xAA) 返回不正确的服务器名称
> -   不支持数据库名称中的特殊字符 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支持
> -   错误消息将始终显示在英语，而不考虑语言设置 （与 Azure 相同） 
  
## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新增内容[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 有关 ODBC Driver 13.1[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]增加了对支持[始终加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)和[Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)时与 Microsoft SQL Server 2016 结合使用。  共用的关键字/属性的说明中的相应连接[驱动程序感知中的连接池 ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新增内容[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 ODBC Driver 13 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]包括以前的功能，从 ODBC Driver 11 for SQL Server 并添加对 Microsoft SQL Server 2016 的支持。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新增内容[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 ODBC Driver 11 for SQL Server 包含新[功能](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)以及在 SQL Server 2012 Native Client 的 ODBC 随附的所有功能。  
