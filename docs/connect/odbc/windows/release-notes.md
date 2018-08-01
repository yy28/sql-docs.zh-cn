---
title: 发行说明 （SQL Server ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 7
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 0e99381224c03bf185044d57cc4b415fcfaedd3b
ms.sourcegitcommit: 9229fb9b37616e0b73e269d8b97c08845bc4b9f3
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2018
ms.locfileid: "39024223"
---
# <a name="release-notes"></a>发行说明
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Windows 上的 Microsoft ODBC Driver for SQL Server 发行说明。  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中的新增功能

**添加功能**:

Azure SQL 数据库和 SQL Server 的数据分类

[Bug 修复](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中的新增功能

**添加功能**:

为支持`SQL_COPT_SS_CEKCACHETTL`和`SQL_COPT_SS_TRUSTEDCMKPATHS`连接属性 (有关详细信息，请参阅[SQL Server 的 ODBC 驱动程序中使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 允许控制的列加密密钥在本地缓存中存在的时间，以及刷新它
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 允许应用程序限制为仅使用指定的列表的列主密匙的 AE 操作


Azure Active Directory 交互式身份验证支持

[Bug 修复](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中的新增功能

**添加功能**:

Always Encrypted 支持 BCP api

新的连接字符串属性 UseFMTOnly 导致驱动程序在特殊情况下要求临时表中使用旧的元数据。

对 Azure SQL 托管实例 （扩展个人预览版） 的支持。 
> [!NOTE]
> 使用托管实例时，有一些差异：
> -   不支持 FILESTREAM 
> -   本地文件系统访问不受支持，但是需要 tracefiles 之类的内容 
> -   从本地创建 UDT 不支持路径 
> -   不支持 Windows 集成身份验证 
> -   不支持 DTC 
> -   sa 帐户不存在 （默认帐户被称为 cloudSA）
> -   TDS 令牌错误 (0xAA) 返回不正确的服务器名称
> -   不支持数据库名称中的特殊字符 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支持
> -   错误消息始终显示在英语中，而无论语言设置 （与 Azure 相同） 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中的新增功能  
 有关 ODBC 驱动程序 13.1[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]添加了对支持[Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)和[Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)与 Microsoft SQL Server 2016 一起使用时。  相应的连接池的关键字/属性中所述[驱动程序注意连接池在 SQL Server 的 ODBC 驱动程序](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中的新增功能  
 ODBC Driver 13 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]包含面向 SQL Server 的 ODBC Driver 11 从以前的功能，并将添加对 Microsoft SQL Server 2016 的支持。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中的新增功能  
 适用于 SQL Server 的 ODBC 驱动程序 11 包含新[功能](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)以及 SQL Server 2012 Native Client 中的 ODBC 随附的所有功能。  
