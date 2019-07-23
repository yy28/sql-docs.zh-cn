---
title: 查看 SQL Server 错误日志 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 35bd9553376b7e8887271a0a51c023a0be95c4de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986627"
---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>查看 SQL Server 错误日志 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含用户定义的事件和某些可用于故障排除的系统事件。 

## <a name="view-the-logs"></a>查看日志

1. 在 SQL Server Management Studio 中选择“对象资源管理器”  。 按 F8 打开“对象资源管理器”  。 或者，在顶部菜单上选择“视图”，然后选择“对象资源管理器”   ：
    
    ![Object_explorer](../../relational-databases/performance/media/object-explorer.png) 

2. 在“对象资源管理器”  中，连接到某个 SQL Server 实例，然后展开该实例。
  
3. 找到并展开“管理”  部分（假设你有权查看它）。

4. 右键单击“SQL Server 日志”，选择“查看”，然后选择“SQL Server 日志”    。

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. 将显示“日志文件查看器”  （可能需要等一段时间），其中包含可供查看的一个日志列表。

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

  ## <a name="see-also"></a>另请参阅
  有关详细信息，请参阅 [MSSQLTips.com](https://www.mssqltips.com/) 上的实用帖[确定 SQL Server 错误日志文件的位置](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/)。

