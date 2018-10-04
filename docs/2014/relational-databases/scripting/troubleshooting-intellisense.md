---
title: IntelliSense 故障排除 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- unavailable options [IntelliSense]
- IntelliSense [SQL Server], troubleshooting
- IntelliSense [SQL Server], unavailable options
- troubleshooting [IntelliSense]
ms.assetid: 4b72ffc6-aea2-4e11-ab36-fa2de4d7bcc5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f18f67aaa142ffeedabfd9269940d28d3fc1ce0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48223761"
---
# <a name="troubleshooting-intellisense-sql-server-management-studio"></a>IntelliSense 故障排除 (SQL Server Management Studio)
  在某些情况下，IntelliSense 选项可能无法按预期要求工作。  
  
## <a name="conditions-that-affect-intellisense"></a>影响 IntelliSense 的状况  
 以下状况可能会影响 IntelliSense 的行为：  
  
-   游标上方出现一个代码错误。  
  
     如果在插入点上方有不完整的语句或其他代码错误，IntelliSense 可能无法分析代码元素，因此不会起作用。 您可以注释掉相应的代码，以再次启用 IntelliSense。  
  
-   插入点在代码注释内。  
  
     如果插入点在源文件中的注释内，则 IntelliSense 选项不可用。  
  
-   插入点在字符串文字内。  
  
     如果插入点在字符串文字周围的引号内，则 IntelliSense 选项不可用，例如：  
  
     `WHERE FirstName LIKE 'Patri%|'`  
  
-   自动选项被禁用。  
  
     默认情况下，许多 IntelliSense 功能都会自动工作，但您可以禁用任何功能。  
  
     即使禁用了自动结束语句功能，仍可以使用 IntelliSense 功能。 有关详细信息，请参阅[配置 IntelliSense (SQL Server Management Studio)](configure-intellisense-sql-server-management-studio.md)。  
  
## <a name="database-engine-query-intellisense"></a>数据库引擎查询 IntelliSense  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 查询编辑器会出现以下问题：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器的 IntelliSense 功能不支持所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法元素。 参数帮助不支持某些对象（例如扩展存储过程）中的参数。 有关详细信息，请参阅 [IntelliSense 支持的 Transact-SQL 语法](transact-sql-syntax-supported-by-intellisense.md)。  
  
-   仅当 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器从 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 或更高版本连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 实例时，才可以使用 IntelliSense。 如果查询编辑器连接到以前版本的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，将无法使用 Intellisense。  
  
-   将 SQLCMD 模式设置为开启时， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中的 IntelliSense 将关闭。  
  
-   IntelliSense 功能不适用于在您的编辑器窗口连接到数据库后由其他连接创建的数据库对象。 如果对象缺少完成列表之类的 IntelliSense 功能，您可以选择以下三种机制之一以便为您的编辑器窗口刷新对象缓存：  
  
    -   依次选择 **“编辑”** 菜单、 **“IntelliSense”** 和 **“刷新本地缓存”**。  
  
    -   使用键盘快捷键 Ctrl+Shift+R。  
  
    -   从 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例中断开您的编辑器窗口，然后重新连接。  
  
-   完成列表不包含您对其没有权限的数据库对象。 IntelliSense 标志会引用您确实拥有其权限的对象。 例如，如果您打开了由他人编写的脚本，则对该人拥有权限而您没有权限的对象的任何引用都会被标记为不正确。  
  
-   如果失去了与 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的连接，完成列表可能会停止工作。 请重新连接到该实例。  
  
  
