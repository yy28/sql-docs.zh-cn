---
title: 查看或更改注册的筛选器和断字符 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], word breakers
- full-text search [SQL Server], filters
- filters [full-text search]
- word breakers [full-text search]
ms.assetid: f88c54df-b1aa-4701-807f-dc92c32363fd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3ae427f9f8d3391d8a8fcd0bff06a6ea3b97044c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375709"
---
# <a name="view-or-change-registered-filters-and-word-breakers"></a>查看或更改注册的筛选器和断字符
  在系统上安装或卸载了任何断字符或筛选器后，所做的更改并不会在服务器实例上自动生效。 本主题介绍在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例上如何查看当前注册的断字符或筛选器，以及如何注册新安装的断字符和筛选器。  
  
### <a name="to-view-a-list-of-languages-whose-word-breakers-are-currently-registered"></a>查看其断字符当前已注册的语言的列表  
  
1.  请使用 [sys.fulltext_languages](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) 目录视图，如下所示：  
  
    ```  
    SELECT * FROM sys.fulltext_languages;   
    ```  
  
### <a name="to-view-a-list-of-the-filters-that-are-currently-registered"></a>查看当前已注册的筛选器的列表  
  
1.  请使用 [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) 系统存储过程，如下所示：  
  
    ```  
    EXEC sp_help_fulltext_system_components 'filter';    
    ```  
  
### <a name="to-register-newly-installed-word-breakers-and-filters"></a>注册新安装的断字符和筛选器  
  
1.  按如下方式使用 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql) 系统存储过程更新语言列表：  
  
    ```  
    exec sp_fulltext_service 'update_languages';   
    ```  
  
### <a name="to-unregister-uninstalled-word-breakers-and-filters"></a>撤消注册已卸载的断字符和筛选器  
  
1.  按如下方式使用 **sp_fulltext_service** 更新语言列表：  
  
    ```  
    exec sp_fulltext_service 'update_languages'  
    ```  
  
2.  按如下方式使用 **sp_fulltext_service** 重新启动筛选器后台程序宿主进程 (fdhost.exe)：  
  
    ```  
    exec sp_fulltext_service 'restart_all_fdhosts';  
    ```  
  
### <a name="to-replace-existing-word-breakers-or-filters-when-installing-new-ones"></a>安装新断字符或筛选器时替换现有的断字符或筛选器  
  
1.  准备安装包含新的断字符或筛选器的 DLL 文件时，请验证其文件名是否不同于已在您的服务器实例上安装的任何现有 DLL 文件的文件名。  
  
2.  将新的 DLL 文件复制到包含该服务器实例的标准 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 文件的目录内。 默认位置是：  
  
     C:\Program Files\Microsoft SQL Server\MSSQL.*instance_name*\MSSQL\Binn  
  
    > [!IMPORTANT]  
    >  强烈建议您仅加载经过签名和验证的组件。 并且，建议您以可能的最低特权运行 FDHOST Launcher (MSSQLFDLauncher) 服务。  
  
3.  安装新的断字符或筛选器。  
  
     **安装并加载 Microsoft Filter Pack IFilter**  
  
    -   [如何将 Microsoft Filter Pack IFilter 注册到 SQL Server](https://go.microsoft.com/fwlink/?LinkId=130439)  
  
4.  按如下方式使用 **sp_fulltext_service** 加载服务器实例中新安装的断字符和筛选器：  
  
    ```  
    EXEC sp_fulltext_service @action='load_os_resources', @value=1;  
    ```  
  
5.  按如下方式使用 **sp_fulltext_service** 更新语言列表：  
  
    ```  
    EXEC sp_fulltext_service 'update_languages';  
    ```  
  
6.  按如下方式使用 **sp_fulltext_service** 重新启动筛选器后台程序宿主进程 (fdhost.exe)：  
  
    ```  
    EXEC sp_fulltext_service 'restart_all_fdhosts';   
    ```  
  
## <a name="see-also"></a>请参阅  
 [设置用于全文筛选器后台程序启动器的服务帐户](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [配置和管理搜索筛选器](configure-and-manage-filters-for-search.md)   
 [配置和管理断字符和词干分析器以便搜索](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
