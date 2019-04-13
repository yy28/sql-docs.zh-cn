---
title: 使用配置管理的 WMI 提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 20a34f01908333650a4c5b566ccab2221a4e07c2
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542117"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>使用 WMI 提供程序进行配置管理

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

本文提供有关如何使用 WMI 提供程序的编程计算机管理的指南。

## <a name="binding"></a>Binding  
 用于配置管理的 WMI 提供程序是一个 COM 对象模型，它支持早期绑定和后期绑定。 借助后期绑定，您可以使用脚本语言（如 VBScript）以编程方式操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络设置和别名。  
  
## <a name="specifying-a-connection-string"></a>指定连接字符串

应用程序通过连接到 WMI 提供程序所定义的 WMI 命名空间，将用于配置管理的该提供程序定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 Windows WMI 服务将此命名空间映射到提供程序 DLL，并将 DLL 加载到内存。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例均由一个 WMI 命名空间表示。

命名空间的默认设置为以下格式。 在格式中，`VV`是 SQL Server 的主版本号。 通过运行数是可发现`SELECT @@VERSION;`。

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

当你使用 PowerShell 连接，前导`\\.\`必须删除。 例如，以下 PowerShell 代码列出所有 WMI 类的 SQL Server 2016 中，这是主版本 13。

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

您可以使用以下 PowerShell 代码来查询所有可用的 WMI ComputerManagement 命名空间。

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **注意：** 如果通过 Windows 防火墙进行连接，需要确保已正确配置您的计算机。 请参阅"通过 Windows 防火墙连接"文章中的 Windows Management Instrumentation 文档[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN[网站](https://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="permissions-and-server-authentication"></a>权限和服务器身份验证  
 若要访问用于配置管理的 WMI 提供程序，客户端 WMI 管理脚本必须在目标计算机上的管理员上下文中运行。 您需要具有要管理的计算机上的本地 Windows Administrators 组的成员身份。  
  
 管理员可以设置组策略以控制用户对 WMI 提供程序的访问。 有关设置组策略的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器帮助中的“组策略和 MMC”。  
  
 WMI 管理脚本可用于更新运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务所使用的帐户。  
  
 用于配置管理的 WMI 提供程序支持安全证书。 有关证书的详细信息，请参阅[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)  
  
  
