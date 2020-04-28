---
title: 使用 VBScript 访问 WMI 提供程序
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a5415e9d425087f42e3058328f061660ffbe8c1e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "73658954"
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>使用 VBScript 访问用于配置管理的 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本部分介绍如何创建一个 VBScript 程序，用于列出计算机上运行的已安装[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的版本。  
  
 代码示例列出了运行在计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例及其版本。  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>列出 SQL Server 的已安装实例的名称和版本  
  
1.  在文本编辑器（如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 记事本）中，打开一个新文档。 复制采用此过程的代码，并用 .vbs 扩展名保存该文件。 此示例名为 test.vbs。  
  
2.  连接到 WMI 提供程序的实例，以便使用 VBScript `GetObject` 函数进行计算机管理。 此示例连接到名为 mpc 的远程计算机，但在连接本地计算机时省略了计算机名称 winmgmts:root\Microsoft\SqlServer\ComputerManagement。 有关 `GetObject` 函数的详细信息，请参阅 VBScript 参考。  
  
3.  使用 `InstancesOf` 方法枚举一组服务。 还可以使用简单的 WQL 查询和 `ExecQuery` 方法代替 `InstancesOf` 方法枚举这些服务。  
  
4.  使用 `ExecQuery` 方法和 WQL 查询检索 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已安装实例的名称和版本。  
  
5.  保存该文件。  
  
6.  在命令提示符下键入**cscript** test.txt 来运行该脚本。  

## <a name="example"></a>示例  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
