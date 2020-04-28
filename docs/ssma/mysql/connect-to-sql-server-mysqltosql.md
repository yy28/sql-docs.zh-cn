---
title: 连接到 SQL Server （MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d73abd3a-80df-4293-b973-1723069db049
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8dc64c84a8d14ea86893d52044894e0af2b1a3bb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103214"
---
# <a name="connect-to-sql-server-mysqltosql"></a>连接到 SQL Server (MySQLToSQL)
使用 "**连接到 SQL Server** " 对话框连接到要迁移到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 若要访问 "**连接到 SQL Server** " 对话框，请在 "**文件**" 菜单上，单击 "**连接到 SQL Server**"。  
  
## <a name="options"></a>选项  
**服务器名称**  
输入或选择要连接到 SQL Server 的实例。 默认情况下，将显示您最近连接的实例。  
  
-   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或句点（**.**）。  
  
-   如果要连接到另一台计算机上的默认实例，请输入计算机的名称。  
  
-   如果要连接到另一台计算机上的命名实例，请输入计算机名称、反斜杠和实例名称，例如*MyServer*\\*MyInstance*。  
  
**服务器端口**  
如果的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例未配置为接受默认端口上的连接（1433），请输入端口号。 否则，请将此值留空。  
  
**Database**  
指定要将对象和数据迁移到的数据库。 当重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，此选项不可用。  
  
**身份验证**  
选择用于连接的身份验证方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要使用当前的 Windows 帐户，请选择 "Windows 身份验证"。 若要指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和密码， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]请选择 "身份验证"。  
  
**用户名**  
如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的是身份验证，请输入该实例的登录[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名。 如果使用的是 Windows 身份验证，则此选项不可用。  
  
**密码**  
如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的是身份验证，请输入该实例上的登录名的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]密码。 如果使用的是 Windows 身份验证，则此选项不可用。  
  
**加密连接**  
如果希望安全地连接到 SQL Server，请通过选中 "**加密连接**" 复选框来使用加密连接。  
  
**信任服务器证书**  
如果要使用此选项，请选中 "**信任服务器证书**" 复选框。  
  
> [!NOTE]  
> 若要启用**信任服务器证书**，必须将 "加密" 设置为**True**。  
  
