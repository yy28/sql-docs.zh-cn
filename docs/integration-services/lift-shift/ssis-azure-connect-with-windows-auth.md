---
title: "使用 Windows 身份验证连接到本地数据源和 Azure 文件共享 | Microsoft Docs"
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0f5e1e2319e58e9013b1f67e8a81efa9a07d556
ms.sourcegitcommit: 6bbecec786b0900db86203a04afef490c8d7bfab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>使用 Windows 身份验证连接到本地数据源和 Azure 文件共享
本文介绍如何将 Azure SQL 数据库上的 SSIS 目录配置为运行以下包：使用 Windows 身份验证连接到本地数据源和 Azure 文件共享的包。 可以使用 Windows 身份验证连接到本地和 Azure 虚拟机以及 Azure 文件中与 Azure SSIS Integration Runtime 位于同一虚拟网络的数据源。

按照本文中的步骤操作时提供的域凭据适用于 SQL 数据库实例上的所有包执行，直至更改或删除这些凭据。

## <a name="provide-domain-credentials-for-windows-authentication"></a>提供 Windows 身份验证的域凭据
若要提供域凭据，让包使用 Windows 身份验证连接到本地数据源，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具连接到托管 SSIS 目录数据库 (SSISDB) 的 SQL 数据库。 有关详细信息，请参阅[连接到 Azure 上的 SSISDB 目录数据库](ssis-azure-connect-to-catalog-database.md)。

2.  将 SSISDB 设置为当前数据库后，打开一个查询窗口。

3.  运行以下存储过程，并提供相应的域凭据：

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  运行 SSIS 包。 这些包使用所提供的凭据通过 Windows 身份验证连接到本地数据源。

### <a name="view-domain-credentials"></a>查看域凭据
若要查看可用的域凭据，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具连接到托管 SSIS 目录数据库 (SSISDB) 的 SQL 数据库。

2.  将 SSISDB 设置为当前数据库后，打开一个查询窗口。

3.  运行以下存储过程，并检查输出：

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>清除域凭据
若要清除和删除按本文所述提供的凭据，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具连接到托管 SSIS 目录数据库 (SSISDB) 的 SQL 数据库。

2.  将 SSISDB 设置为当前数据库后，打开一个查询窗口。

3.  运行以下存储过程：

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-an-on-premises-sql-server"></a>连接到本地 SQL Server
若要检查能否连接到本地 SQL Server，请执行以下操作：

1.  若要运行此测试，请找一台未加入域的计算机。

2.  在未加入域的计算机上，运行以下命令，以通过要使用的域凭据启动 SQL Server Management Studio (SSMS)：

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  从 SSMS 中，检查能否连接到要使用的本地 SQL Server。

### <a name="prerequisites"></a>先决条件
若要从 Azure 上运行的包连接到本地 SQL Server，必须启用以下先决条件：

1.  在 SQL Server 配置管理器中，启用 TCP/IP 协议。
2.  允许通过 Windows 防火墙进行访问。 有关详细信息，请参阅[配置 Windows 防火墙以允许 SQL Server 访问](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access)。
3.  若要与 Windows 身份验证连接，请确保 Azure-SSIS Integration Runtime 属于还包含本地 SQL Server 的虚拟网络 (VNet)。  有关详细信息，请参阅[将 Azure-SSIS 集成运行时联接到虚拟网络](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)。 然后使用 `catalog.set_execution_credential` 提供凭据，如本文中所述。

## <a name="connect-to-an-on-premises-file-share"></a>连接到本地文件共享
若要检查能否连接到本地文件共享，请执行以下操作：

1.  若要运行此测试，请找一台未加入域的计算机。

2.  在未加入域的计算机上运行以下命令。 此命令会打开一个命令提示符窗口，其中包含要使用的域凭据，然后通过获取目录列表测试与文件共享的连接性。

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  检查该目录列表是不是为要使用的本地文件共享返回的。

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>连接到 Azure VM 上的文件共享
若要连接到 Azure 虚拟机上的文件共享，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具连接到托管 SSIS 目录数据库 (SSISDB) 的 SQL 数据库。

2.  将 SSISDB 设置为当前数据库后，打开一个查询窗口。

3.  按以下选项中所述运行 `catalog.set_execution_credential` 存储过程：

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>连接到 Azure 文件中的文件共享
有关 Azure 文件的详细信息，请参阅 [Azure 文件](https://azure.microsoft.com/services/storage/files/)。

若要连接到 Azure 文件共享上的文件共享，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具连接到托管 SSIS 目录数据库 (SSISDB) 的 SQL 数据库。

2.  将 SSISDB 设置为当前数据库后，打开一个查询窗口。

3.  按以下选项中所述运行 `catalog.set_execution_credential` 存储过程：

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>后续步骤
- 部署包。 有关详细信息，请参阅[使用 SQL Server Management Studio (SSMS) 部署 SSIS 项目](../ssis-quickstart-deploy-ssms.md)。
- 运行包。 有关详细信息，请参阅[使用 SQL Server Management Studio (SSMS) 运行 SSIS 包](../ssis-quickstart-run-ssms.md)。
- 计划包执行。 有关详细信息，请参阅[计划 Azure 上的 SSIS 包执行](ssis-azure-schedule-packages.md)。
