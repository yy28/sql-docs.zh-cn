---
title: 在命令提示符下运行数据库实验助手
description: 在命令提示符下运行数据库实验助手
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: c3b87eafa460cfef69666a3837f56626dab81d47
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056573"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt-sql-server"></a>在命令提示符下运行数据库实验助手（SQL Server）

本文介绍如何使用 "命令提示符" 窗口在数据库实验助手（DEA）中捕获跟踪，然后对结果进行分析。 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令启动新的工作负荷捕获

若要启动新的工作负荷捕获，请运行以下命令：

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**示例**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>重播工作负荷

1.  登录到 Distributed Replay 控制器计算机。
2.  使用 DEA 命令将捕获的工作负载跟踪转换为 IRF 文件：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  使用 StartReplayCaptureTrace 在运行 SQL Server 的目标计算机上启动跟踪捕获。
       
    A.  在 SQL Server Management Studio （SSMS）中，打开 < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql。
    
    b.  运行 `Set @durationInMins=0`，以使跟踪捕获不会在指定的时间后自动停止。
    
    c.  若要设置每个跟踪文件的最大文件大小，请运行 `Set @maxfilesize`。 建议的大小为200（以 MB 为单位）。
    
    d.  编辑 `@Tracefile` 以设置跟踪文件的唯一名称。
    
    e.  如果只能在特定数据库上捕获工作负荷，请编辑 `@dbname` 以指定数据库名称。 默认情况下，将捕获整个服务器上的工作负荷。 
4.  针对目标 SQL Server 实例重播 IRF 文件：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    A.  若要监视状态，请打开命令提示符窗口并运行 `DReplay status -f 1`。
        
    b.  若要停止重播（例如，如果发现 pass% 低于预期），请打开命令提示符窗口并运行 `DReplay cancel`。

5.  停止目标 SQL Server 实例上的跟踪捕获。
6.  在 SSMS 中，打开 `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`。
7.  编辑 `@Tracefile` 以匹配运行 SQL Server 的目标计算机上的跟踪文件路径。
8.  针对运行 SQL Server 的目标计算机运行脚本。

## <a name="analyze-traces-by-using-the-dea-command"></a>使用 DEA 命令分析跟踪

若要启动新的跟踪分析，请运行以下命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**示例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>后续步骤

有关 DEA 和演示的19分钟简介，请观看以下视频：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
