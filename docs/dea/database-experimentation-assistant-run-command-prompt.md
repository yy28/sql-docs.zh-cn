---
title: 对于 SQL Server 升级的命令提示符下运行数据库实验助手
description: 在命令提示符下运行数据库实验助手
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: e18cbe09ec9394ffb3c57c5ffcffc788278cc374
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011593"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>在命令提示符下运行数据库实验助手

本文介绍如何使用命令提示符窗口中捕获的跟踪中数据库实验助手 (DEA)，然后分析结果。 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令启动新的工作负荷捕获

若要启动新的工作负荷捕获，请运行以下命令：

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**示例**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>重播工作负荷

1.  登录到 Distributed Replay 控制器计算机。
2.  将转换的工作负荷跟踪捕获到 IRF 文件使用 DEA 命令：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  通过使用 StartReplayCaptureTrace.sql 运行 SQL Server 的目标计算机上启动跟踪捕获。
       
    a.  在 SQL Server Management Studio (SSMS)，打开 < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql。
    
    b.  运行`Set @durationInMins=0`，以便跟踪捕获不会在指定时间后自动停止。
    
    c.  若要设置每个跟踪文件的最大文件大小，请运行`Set @maxfilesize`。 建议的大小为 200 （以 mb 为单位）。
    
    d.  编辑`@Tracefile`设置跟踪文件的唯一名称。
    
    e.  编辑`@dbname`如果工作负荷必须捕获仅在特定数据库上指定的数据库名称。 默认情况下，捕获整个服务器上的工作负荷。 
4.  重播目标 SQL Server 实例针对 IRF 文件：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  若要监视状态，请打开命令提示符窗口并运行`DReplay status -f 1`。
        
    b.  若要停止重播，例如像您看到传递 %是低于预期，打开命令提示符窗口并运行`DReplay cancel`。

5.  目标 SQL Server 实例上停止跟踪捕获。
6.  在 SSMS 中，打开`<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`。
7.  编辑`@Tracefile`以匹配在运行 SQL Server 的目标计算机上的跟踪文件路径。
8.  对运行 SQL Server 的目标计算机运行该脚本。

## <a name="analyze-traces-by-using-the-dea-command"></a>通过使用 DEA 命令分析跟踪

若要启动新的跟踪分析，请运行以下命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**示例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>后续步骤

DEA 和演示的 19 分钟介绍，请观看以下视频：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
