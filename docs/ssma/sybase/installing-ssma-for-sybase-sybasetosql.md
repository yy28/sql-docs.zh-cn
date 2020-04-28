---
title: 为 SAP ASE 安装 SSMA （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 91a4dfcf8add3900c51e33a6e40fa874ce9f9798
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028971"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>安装 SSMA for SAP ASE （SybaseToSQL）
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]适用于 SAP 自适应服务器企业（ASE）的迁移助手（SSMA）包含一个客户端应用程序，该应用程序可用于执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从 SAP ASE 到或 Azure SQL 数据库的迁移。 它还包含一个扩展包，支持数据迁移，并在迁移的数据库中使用 ASE 系统功能。  
  
在计划执行迁移步骤的计算机上安装客户端应用程序。 在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]迁移了迁移数据库的计算机上安装扩展包文件。  
  
## <a name="upgrading-ssma-for-sap-ase"></a>升级 SSMA for SAP ASE  
如果要升级到更高版本的 SSMA for SAP ASE，则必须先卸载客户端和服务器扩展包。 然后安装较新的版本。  
  
如果从早期版本的 SSMA for SAP ASE 打开项目，SSMA 会询问你是否要将项目转换为较新版本。 单击 **"是"** 以使用 SSMA 的较新版本中的项目。  
  
## <a name="contents"></a>目录  
  
|项目|说明|  
|---------|---------------|  
|[安装 SSMA for SAP ASE 客户端 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|提供有关安装 SSMA for SAP ASE 客户端的信息和说明。|  
|[在 SQL Server 上安装 SSMA 组件 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|提供有关在的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上安装扩展包的和说明的信息。|  
|[删除 SSMA for SAP ASE 组件 &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|提供有关卸载客户端程序和扩展包的说明。|  
  
## <a name="see-also"></a>另请参阅  
[将 SAP ASE 数据库迁移到 SQL Server-Azure SQL 数据库 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
