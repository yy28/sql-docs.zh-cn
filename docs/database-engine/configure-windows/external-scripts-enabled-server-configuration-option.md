---
title: 启用了外部脚本的服务器配置选项 | Microsoft Docs
ms.date: 11/13/2017
ms.prod: sql
ms.technology: configuration
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2108f68e6eb73ae447326eac0be008e042b05119
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693318"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>启用了外部脚本的服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
适用范围：[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

使用 **external scripts enabled** 选项启用包含某些远程语言扩展的脚本执行。 此属性默认处于禁用状态。 安装“高级分析服务”后，安装程序可以根据需要将此属性设置为 true。

## <a name="remarks"></a>Remarks

在使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 过程执行外部脚本之前，必须启用“已启用外部脚本”选项。 使用 sp_execute_external_script 执行以受支持的语言（如 R 或 Python）编写的脚本。 

+ 对于 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中的 R 语言，以及一组 R 工作站工具和连接库。

    在 **安装程序安装期间安装** 高级分析扩展 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，以启用 R 脚本的执行。 默认安装 R 语言。

+ 对于 [[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 使用与 SQL Server 2016 相同的体系结构，但支持 Python 语言。

    在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中安装“高级分析扩展”功能，以启用外部脚本的执行。 确保在初始安装过程中至少选择一种语言：R 和/或 Python。 

## <a name="additional-requirements"></a>其他需求

安装后，要启用外部脚本，请执行下面的脚本：

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

你必须重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以使此更改生效。

有关详细信息，请参阅[安装 SQL Server 机器学习](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。

## <a name="see-also"></a>另请参阅

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)

[sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

[SQL Server 机器学习服务](../../advanced-analytics/r/sql-server-r-services.md)
