---
title: 安装适用于 SAP ASE (SybaseToSQL) SSMA |Microsoft 文档
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 336012819c23b02ac0527a70da930c5b74686e7a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>安装适用于 SAP ASE (SybaseToSQL) SSMA
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 的 SAP 自适应 Server Enterprise (ASE) 包含的客户端应用程序用于从 SAP ASE 来执行迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 它还包含已迁移数据库中支持数据迁移和 ASE 系统函数的使用的扩展包。  
  
在你计划执行迁移步骤的计算机上安装客户端应用程序。 安装运行的计算机上的扩展包文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]已迁移的数据库是承载。  
  
## <a name="upgrading-ssma-for-sap-ase"></a>升级 SSMA for SAP ASE  
如果你想要升级到更高版本的 SSMA for SAP ASE，必须先卸载客户端和服务器扩展包。 然后安装较新版本。  
  
如果 SAP ASE 从早期版本的 SSMA 打开项目，则会要求 SSMA，如果你想要将项目转换为较新版本。 单击**是**用于 SSMA 的较新版本中的项目。  
  
## <a name="contents"></a>目录  
  
|项目|Description|  
|---------|---------------|  
|[为 SAP ASE 客户端安装 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|提供有关安装 SSMA for SAP ASE 客户端有关的信息和说明。|  
|[在 SQL Server 上安装 SSMA 组件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|提供有关的信息和说明的实例上安装的扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[为 SAP ASE 组件删除 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|提供用于卸载客户端的说明程序和扩展包。|  
  
## <a name="see-also"></a>另请参阅  
[迁移 SAP ASE 数据库移到 SQL Server 的 Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
