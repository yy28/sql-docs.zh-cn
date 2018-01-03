---
title: "全局设置 （日志记录） (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12dbcd77-2b90-4fa1-9cf9-239231ea5773
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: d5e0cab604baad282c06367e3271915329d358b7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="global-settings-logging-oracletosql"></a>全局设置 （日志记录） (OracleToSQL)
使用**全局设置**对话框中，指定 SSMA 的日志记录设置。 通常情况下，仅当使用产品支持时，才会更改这些设置。  
  
若要访问此对话框中，在**工具**菜单上，选择**全局设置**，然后单击**日志记录**在左窗格的底部的按钮。  
  
## <a name="options"></a>“常规”  
**消息级别**  
下下面的选项将可用**消息级别**:  
  
|选项|Description|  
|----------|---------------|  
|**[所有类别]**|用于设置以下选项的所有日志记录级别。|  
|**收集器**|收集有关源架构的元数据并将其保存到项目。|  
|**转换器**|将结构的源数据库对象，如表和存储的过程转换为相应[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]结构。|  
|**数据迁移器**|将数据迁移从源数据库到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|**格式化程序**|子组件的生成的脚本的转换器[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构。|  
|**图形用户界面**|当你使用 SSMA 工具时显示的消息。|  
|**链接器**|解析的 SQL 标识符，并提供到其他组件的信息。|  
|**其他**|不在任何其他类别的所有消息。|  
|**分析器**|分析源架构。|  
|**同步器**|加载源到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|**TreeConverter**|将转换到的源元数据中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据。|  
|**测试人员**|当你使用 SSMA 测试人员时显示的消息。|  
  
每个选项下**消息级别**，为 SSMA 配置以下日志记录级别之一：  
  
|||  
|-|-|  
|**错误**|仅错误消息写入日志。|  
|**错误**|错误消息和错误消息写入日志。|  
|**警告**|警告、 错误和错误消息写入日志。|  
|**信息**|信息性、 警告、 错误消息和错误消息写入日志。|  
|**调试**|将所有消息，包括调试消息写入日志的都写入。|  
  
**日志文件路径**  
文件路径和名称的 SSMA 日志文件。 若要指定其他名称，单击当前路径中，，然后单击浏览 (**...**) 按钮。  
  
**日志文件大小**  
以 kb 为单位的日志文件最大大小。 最小大小为 10 KB。 默认大小为 10240 KB。  
  
**日志文件的总数**  
当一个日志已满时，SSMA 将重命名日志文件，并启动一个新的活动。 通过使用此设置，指定日志文件，使最大数量。 最小值为 2。  
  
