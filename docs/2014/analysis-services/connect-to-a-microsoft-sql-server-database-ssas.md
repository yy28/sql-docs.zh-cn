---
title: 连接到 Microsoft SQL Server 数据库 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserverdb.f1
ms.assetid: 6ebfe029-dbba-4f0d-a556-328e79ef629f
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50dcb1cfa930a6fd09ff1f25d91b4ad4e5b42acb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189454"
---
# <a name="connect-to-a-microsoft-sql-server-database-ssas"></a>连接到 Microsoft SQL Server 数据库 (SSAS)
  **“表导入向导”** 的这一页可用于指定用于连接到 Microsoft SQL Server 数据库的设置。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到数据源，必须在计算机上安装适当的访问接口。  
  
> [!NOTE]  
>  在此页中选择数据库时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选数据库中读取，则导入将不会成功。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **友好连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **服务器名称**  
 选择要连接到的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称或者键入其名称或 IP 地址。  
  
 可以使用句点 (.)、(local) 或 localhost 来指示本地服务器。  
  
 **Use Windows Authentication**  
 指定是否使用 Windows 身份验证来连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的实例。  
  
 Windows 身份验证模式允许用户通过使用 Windows 用户帐户进行连接。 请尽可能使用 Windows 身份验证。  
  
 在使用 Windows 身份验证时，在“表格属性”窗口和“导入向导”中预览和筛选数据时，也使用当前用户的凭据。 这些凭据不用于导入或刷新数据；而是使用在“模拟信息”页中指定的 Windows 凭据。  
  
 **Use SQL Server Authentication**  
 指定是否使用 SQL Server 身份验证来连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的实例。  
  
 若使用 SQL Server 身份验证，SQL Server 将通过检查是否已设置 SQL Server 登录帐户以及指定的密码是否与以前记录的密码匹配，自行进行身份验证。  
  
 使用 SQL Server 身份验证构造数据源的连接字符串。 在“表格属性”窗口和“导入向导”中预览和筛选数据时，也使用这些凭据。 这些凭据不用于导入或刷新数据；而是使用在“模拟信息”页中指定的 Windows 凭据。  
  
 **用户名**  
 为数据库连接指定用户名。 只有在已选择使用 SQL Server 身份验证进行连接的情况下，此选项才可用。  
  
 **密码**  
 为数据库连接指定密码。 只有在已选择使用 SQL Server 身份验证进行连接的情况下，此选项才是可编辑的。  
  
 **保存我的密码**  
 指定是否存储已在“密码”框中输入的密码。 只有在已选择使用 SQL Server 身份验证进行连接的情况下，此选项才可用。  
  
 **数据库名称**  
 从数据库列表中选择数据库。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。 有关详细信息，请参阅[设置高级属性 (SSAS)](set-advanced-properties-ssas.md)。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  
