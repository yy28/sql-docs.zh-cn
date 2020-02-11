---
title: 使用 WMI 提供程序进行配置管理
ms.custom: seo-lt-2019
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
ms.openlocfilehash: d76cc006e2f8638de9b6d3c21660806239022ec0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73657377"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>使用 WMI 提供程序进行配置管理

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

本文提供了有关如何通过 WMI 提供程序进行计算机管理的指南。

## <a name="binding"></a>绑定  
 用于配置管理的 WMI 提供程序是一个 COM 对象模型，它支持早期绑定和后期绑定。 借助后期绑定，您可以使用脚本语言（如 VBScript）以编程方式操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络设置和别名。  
  
## <a name="specifying-a-connection-string"></a>指定连接字符串

应用程序通过连接到 WMI 提供程序所定义的 WMI 命名空间，将用于配置管理的该提供程序定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 Windows WMI 服务将此命名空间映射到提供程序 DLL，并将该 DLL 加载到内存中。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例均由一个 WMI 命名空间表示。

命名空间默认为以下格式。 格式`VV`是 SQL Server 的主版本号。 此数字可通过运行`SELECT @@VERSION;`发现。

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

使用 PowerShell 进行连接时，必须删除该`\\.\`前导。 例如，下面的 PowerShell 代码列出了2016版（主要版本为13）的所有 WMI 类 SQL Server。

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

可以使用以下 PowerShell 代码查询所有可用的 WMI ComputerManagement 命名空间。

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **注意：** 如果要通过 Windows 防火墙进行连接，则需要确保计算机配置正确。 请[参阅 MSDN 网站](https://go.microsoft.com/fwlink/?linkid=15426)上[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation 文档中的 "通过 Windows 防火墙连接" 一文。  
  
## <a name="permissions-and-server-authentication"></a>权限和服务器身份验证  
 若要访问用于配置管理的 WMI 提供程序，客户端 WMI 管理脚本必须在目标计算机上的管理员上下文中运行。 您需要具有要管理的计算机上的本地 Windows Administrators 组的成员身份。  
  
 管理员可以设置组策略以控制用户对 WMI 提供程序的访问。 有关设置组策略的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器帮助中的“组策略和 MMC”。  
  
 WMI 管理脚本可用于更新运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务所使用的帐户。  
  
 用于配置管理的 WMI 提供程序支持安全证书。 有关证书的详细信息，请参阅[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)  
  
  
