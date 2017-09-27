---
title: "连接到本地数据源使用 Windows 身份验证 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 25113093ccd068a9afe661e160ae3319025b7534
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="connect-to-on-premises-data-sources-with-windows-authentication"></a>连接到本地数据源使用 Windows 身份验证
本文介绍如何配置 Azure SQL 数据库运行使用 Windows 身份验证连接到本地数据源的包上的 SSIS 目录。

提供当你按照本文中的步骤的域凭据应用到 SQL Database 实例上的所有包执行，直至你更改或删除凭据。

## <a name="prerequisite"></a>前提条件
为 Windows 身份验证设置域凭据之前，请检查非加入域的计算机可以连接到你本地数据源中`runas`模式。 例如，若要检查你是否可以连接到本地 SQL Server，请执行以下操作：

1.  若要运行此测试，fFind 非加入域的计算机。

2.  在非加入域的计算机上，运行以下命令以启动 SQL Server Management Studio (SSMS) 具有你想要使用的域凭据：

   ```cmd
   runas.exe /netonly /user:<domain>\<username> SSMS.exe
   ```

3.  从 SSMS 中，请检查你是否可以连接到你想要使用本地 SQL Server。

## <a name="provide-domain-credentials"></a>提供域凭据
若要提供让使用 Windows 身份验证连接到本地数据源的包的域凭据，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或另一种工具，连接到 SQL 数据库承载 SSIS 目录数据库 (SSISDB)。 有关详细信息，请参阅[连接到 Azure 上的 SSISDB 目录数据库](ssis-azure-connect-to-catalog-database.md)。

2.  使用为当前数据库的 SSISDB，打开查询窗口。

3.  运行以下存储的过程，并提供适当的域凭据：

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  运行 SSIS 包。 包使用您提供连接到本地数据源使用 Windows 身份验证的凭据。

## <a name="view-domain-credentials"></a>视图域凭据
若要查看活动的域凭据，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或另一种工具，连接到 SQL 数据库承载 SSIS 目录数据库 (SSISDB)。

2.  使用为当前数据库的 SSISDB，打开查询窗口。

3.  运行以下存储的过程，然后检查输出：

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

## <a name="clear-domain-credentials"></a>清除域凭据
若要清除和删除你提供这篇文章中所述的凭据，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或另一种工具，连接到 SQL 数据库承载 SSIS 目录数据库 (SSISDB)。

2.  使用为当前数据库的 SSISDB，打开查询窗口。

3.  运行以下存储的过程：

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="next-steps"></a>后续步骤
- 部署包。 有关详细信息，请参阅[部署的 SSIS 项目与 SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md)。
- 运行的包。 有关详细信息，请参阅[运行 SSIS 包与 SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md)。
- 计划包。 有关详细信息，请参阅[计划 SSIS 包在 Azure 上的执行](ssis-azure-schedule-packages.md)

