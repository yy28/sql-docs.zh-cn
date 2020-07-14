---
title: 数据库属性（“事务日志传送”页）| Microsoft Docs
description: 使用“数据库属性”对话框中的“事务日志传送”选项卡，将数据库启用为日志传送主数据库并设置其选项。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.f1
ms.assetid: 72c4e539-fe11-4d57-b977-65b418d5916f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 75c87efd24b1e345cb99413d1a524e872f0eb022
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85630970"
---
# <a name="database-properties-transaction-log-shipping-page"></a>数据库属性（“事务日志传送”页）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  使用此页可以配置和修改数据库的日志传送属性。  
  
 有关日志传送概念的说明，请参阅 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
## <a name="options"></a>选项  
 **将此数据库启用为日志传送配置中的主数据库**  
 将此数据库启用为日志传送的主数据库。 请选中该选项，然后再配置此页上的剩余选项。 如果清除此复选框，则将删除此数据库的日志传送配置。  
  
 **备份设置**  
 单击“备份设置”可以配置备份计划、位置、警报和存档参数。  
  
 **备份计划**  
 显示当前为主数据库选择的备份计划。 单击 **“备份设置”** 可修改这些设置。  
  
 **上次备份创建时间**  
 指示上次对主数据库进行事务日志备份的时间和日期。  
  
 **辅助服务器实例和数据库**  
 列出当前为此主数据库配置的辅助服务器和数据库。 突出显示某个数据库，然后单击 **“...”** 可以修改与该辅助数据库相关联的参数。  
  
 **添加**  
 单击“添加”可以向此主数据库的日志传送配置中添加辅助数据库。  
  
 **删除**  
 从此日志传送配置中删除所选数据库。 首先选择该数据库，再单击 **“删除”** 。  
  
 **使用监视服务器实例**  
 为此日志传送配置设置监视服务器实例。 选中 **“使用监视服务器实例”** 复选框，再单击 **“设置”** 可以指定监视服务器实例。  
  
 **监视服务器实例**  
 指示当前为该日志传送配置设置的监视服务器实例。  
  
 **设置**  
 为日志传送配置设置监视服务器实例。 单击 **“设置”** 可以配置此监视服务器实例。  
  
 **编写配置脚本**  
 生成一个脚本，使用所选参数配置日志传送功能。 单击 **“编写配置脚本”** ，然后为该脚本选择输出目标。  
  
> [!IMPORTANT]  
>  在编写辅助数据库的脚本设置之前，必须调用 **“辅助数据库设置”** 对话框。 通过调用该对话框，用户可以连接到辅助服务器，并且可以检索生成该脚本所需的辅助数据库的当前设置。  
  
## <a name="see-also"></a>另请参阅  
 [日志传送存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)   
 [日志传送表 (Transact-SQL)](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
