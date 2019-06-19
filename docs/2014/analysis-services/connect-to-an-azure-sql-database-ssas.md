---
title: 连接到 Azure SQL 数据库 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlazure.f1
ms.assetid: 4e0344e9-1822-4698-ad22-05f1f341ced7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9032249e880f11f27edd53e23d4ca54a47b920db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087151"
---
# <a name="connect-to-an-azure-sql-database-ssas"></a>连接到 Azure SQL Database (SSAS)
  “表导入向导”  的这一页可用于连接到 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”** 。  
  
> [!NOTE]  
>  若要连接到 Azure DataMarket 数据集，请参阅[连接到报表或数据馈送 (SSAS)](connect-to-a-report-or-data-feed-ssas.md)。  
  
 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 是一个托管的关系数据库，您可以使用 SQL Server 身份验证连接到该数据库。 有关 [!INCLUDE[ssSDS](../includes/sssds-md.md)]的详细信息，请参阅网站 [SQL Database](https://go.microsoft.com/fwlink/?LinkID=157856)。 若要连接到数据源，必须在计算机上安装适当的访问接口。  
  
> [!NOTE]  
>  在此页中选择数据库时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选数据库中读取，则导入将不会成功。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **友好连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **服务器名称**  
 键入要连接到的服务器的名称或 IP 地址。  
  
 **用户名**  
 为数据库连接指定用户名。  
  
 在为数据源构造连接字符串时，将使用该用户名。 在“表格属性”窗口和“导入向导”中预览和筛选数据时，也使用这些凭据。 这些凭据不用于导入或刷新数据；而是使用在“模拟信息”页中指定的 Windows 凭据。  
  
 **密码**  
 为数据库连接指定密码。  
  
 **保存我的密码**  
 指定是否存储已在“密码”  框中输入的密码。  
  
 **数据库名称**  
 从数据库列表中选择数据库。  
  
 **高级**  
 通过使用“设置高级属性”  对话框设置附加的连接属性。 有关详细信息，请参阅[设置高级属性 (SSAS)](set-advanced-properties-ssas.md)。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  
