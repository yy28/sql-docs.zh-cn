---
title: 配置平面文件目标（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc1a9102a8fa4ee834663ae839940e2db9b469e1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424974"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>配置平面文件目标（SQL Server 导入和导出向导）
  使用 "**配置平面文件目标**" 页可以为目标平面文件指定格式设置选项，并在继续操作前预览结果。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **源平面文件**  
 目标文件的名称。  
  
 **行分隔符**  
 从行分隔符的列表中进行选择。  
  
|“值”|说明|  
|-----------|-----------------|  
|**回车换行符**|行由回车符和换行符的组合分隔。|  
|**回车**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**跟{,}**|行由逗号分隔。|  
|**选项卡 {t}**|行由制表符分隔。|  
|**竖线 {&#124;}**。|行由竖线分隔。|  
  
 **列分隔符**  
 从列分隔符的列表中进行选择。  
  
|“值”|说明|  
|-----------|-----------------|  
|**回车换行符**|列由回车符和换行符的组合分隔。|  
|**回车**|列由回车符分隔。|  
|**{LF}**|列由换行符分隔。|  
|**分号 {;}**|列由分号分隔。|  
|**冒号 {:}**|列由冒号分隔。|  
|**跟{,}**|列由逗号分隔。|  
|**选项卡 {t}**|列由制表符分隔。|  
|**竖线 {&#124;}**。|列由竖线分隔。|  
  
 **预览**  
 在 "**预览数据**" 对话框中查看目标平面文件的所选格式设置选项的结果。  
  
 **编辑转换**  
 使用 "**列映射**" 对话框删除行、追加行并配置目标文件中的列。  
  
  
