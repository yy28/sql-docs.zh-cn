---
title: "SQL Server Data Tools (SSDT) - 候选发布 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 03/09/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13e47d2d-a441-4962-87ec-1c08973bb9e8
caps.latest.revision: 2
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3f784e2f94006992f7b2baac6a16bb960a02d91d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-data-tools-ssdt---release-candidate"></a>SQL Server Data Tools (SSDT) - 候选发布

欢迎使用最新版 SQL Server Data Tools (SSDT) 候选发布 (17.0 RC3)！  此 SQL Server Data Tools (SSDT) 候选发布包括对 [SQL Server vNext](https://msdn.microsoft.com/library/mt788653.aspx) 的支持。 


## <a name="download"></a>下载

不建议将 SSDT 候选发布 17.0 RC3 用于生产。 若要用于生产，建议继续使用[正式发布版本 &#40;16.x&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)
  
![下载](../ssdt/media/download.png)[ 下载 SQL Server Data Tools 17.0 RC3](https://go.microsoft.com/fwlink/?linkid=842523)。  

## <a name="enhancements"></a>增强功能

**数据库项目：**
- 向 SqlPackage 添加了新的命令行选项：ModelFilePath。  这为高级用户提供了一个选项，用于指定外部 model.xml 文件来执行导入、发布和脚本编写操作。   

**IS 项目：**
- 提供针对 SQL Server vNext 的 CDC 控制任务、CDC 拆分器和 CDC 源支持。 

**BI 改进：**

**AS 项目：**
- 改进了向表格模型提交编辑内容（计算列、度量值、导入表等）时 AS 集成工作区的性能
- 针对 PowerQuery 集成全面改进和修复了预览 1400 兼容性级别模型 

**RS 项目：**
- 现在，可使用可嵌入的 RVC 控件以支持 SSRS 2016

## <a name="bug-fixes"></a>Bug 修复
- 解决了 BI 项目的模板优先级问题，使其不在 VS 新项目类别的最上面显示
- 修复了在打开 SSIS、SSAS 或 SSRS 解决方案时极少数情况下发生的 VS 故障

**AS 项目：**

- 解决了无法使用 devenv.com 生成 AS“smproj”文件的问题
- 解决了在 AS 表格模型工作表标签标题中使用朝鲜语输入法时，文本更改过于频繁的问题
- 解决了 DAX Related() 函数的 IntelliSense 无法正常显示其他表中列的问题
- 通过对 AS 数据库的列表进行排序，改进了从数据库对话框执行的 AS 表格项目导入操作
- 解决了在 AS 表格模型中创建计算表时，表达式中没有将表列为建议对象的问题
- 解决了在查看代码后尝试使用集成工作区服务器打开预览 1400 AS 模型时遇到的问题
- 解决了在某些情况下一些数据源（不支持初始目录）无法正常运行的问题 
- 即使启用了保留分区的选项，部署向导也应向计算表分区应用更改
- 解决了只有在重新选择现有 AS 连接的“高级属性”对话框后，才能看到完整列表的问题 

**RS 项目：**

- 解决了在 SSDT 中设计报表时多数更改会导致参数、数据源和数据集的树状视图发生折叠的问题 

**IS 项目：**
- 解决了在创建集成服务项目时看到“表格模型资源管理器”菜单的问题

**数据库项目：**
- SSDT DACPAC 重新部署并添加 IgnoreColumnOrder 设置 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/1221587/ssdt-dacpac-deploy-add-setting-back-in-for-ignorecolumnorder)
- SSDT 在使用 STRING_SPLIT 的情况下会编译失败 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/2906200/ssdt-failing-to-compile-if-string-split-is-used)
- 解决了 DeploymentContributors 有权访问公共模型，但支持架构尚未初始化的问题 [Github 问题](https://github.com/Microsoft/DACExtensions/issues/8)
- FILEGROUP 位置的 DacFx 临时修补程序
- 修复了外部同义词的“未解析的引用”错误。 
- Always Encrypted：联机加密无法禁用对取消项进行更改跟踪，并且如果在开始加密前尚未清除更改跟踪，联机加密也无法正常运行

## <a name="see-also"></a>另请参阅  
[Visual Studio 中的 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 论坛](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 团队博客](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect 反馈](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT 文档](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 参考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
