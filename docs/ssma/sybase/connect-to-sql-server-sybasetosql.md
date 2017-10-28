---
title: "连接到 SQL Server (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 30179b25-409b-4e23-bc73-2f226657098f
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f75b0b545edbf5af08af767b601faadbbc7de76c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-sql-server-sybasetosql"></a>连接到 SQL Server (SybaseToSQL)
使用**连接到 SQL Server**对话框中，连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]你想要迁移到。 访问**连接到 SQL Server**对话框中，在**文件**菜单上，单击**连接到 SQL Server**。  
  
## <a name="options"></a>选项  
**服务器名称**  
输入或选择要连接到的 SQL Server 实例。 默认情况下，显示最近连接到的实例。  
  
-   如果你要连接到本地计算机上的默认实例，可以输入**localhost**或句点 (**。**)。  
  
-   如果你要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
-   如果你要连接到另一台计算机上的命名实例，输入计算机名称、 反斜杠和实例名称，例如*MyServer*\\*MyInstance*。  
  
**服务器端口**  
如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]未配置为接受默认值上的连接端口 (1433)，输入端口号。 否则，将此值留空。  
  
**数据库**  
指定要迁移对象和数据迁移到的数据库。 此选项不可用，当重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**身份验证**  
选择用于连接到的身份验证方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 若要使用您当前的 Windows 帐户，选择 Windows 身份验证。 若要指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名和密码，选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证。  
  
**用户名**  
如果你使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，该实例的输入的登录名[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果使用 Windows 身份验证，则此选项不可用。  
  
**密码**  
如果你使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，在该实例上输入该登录名的密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果使用 Windows 身份验证，则此选项不可用。  
  
**加密连接**  
如果你想要安全地连接到 SQL Server，请通过检查使用的加密连接**加密连接**复选框。  
  
**信任服务器证书**  
如果你想要使用此选项，选择**信任服务器证书**复选框。  
  
> [!NOTE]  
> 若要启用**信任服务器证书**，必须将"加密"设置为**True**。  
  

