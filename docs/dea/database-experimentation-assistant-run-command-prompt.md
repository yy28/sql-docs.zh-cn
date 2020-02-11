---
title: 在命令提示符下运行数据库实验助手
description: 在命令提示符下运行数据库实验助手
ms.custom: seo-lt-2019
ms.date: 01/24/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 8055ae8b66c2f2b59f18b0ee40dcac8753c0eb7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76831749"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>在命令提示符下运行数据库实验助手

本文介绍如何在数据库实验助手（DEA）中捕获跟踪，然后在命令提示符下分析结果。

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令启动新的工作负荷捕获

若要启动新的工作负荷捕获，请在命令提示符下运行以下命令：

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**示例**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>重播工作负荷捕获

1. 登录到 Distributed Replay 控制器计算机。
2. 若要将使用 DEA 命令捕获的工作负荷跟踪转换为 IRF 文件，请在命令提示符下运行以下命令：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. 使用 StartReplayCaptureTrace 在运行 SQL Server 的目标计算机上启动跟踪捕获。

    a.  在 SQL Server Management Studio （SSMS）中，打开 <\>Dea_InstallPath \Scripts\StartReplayCaptureTrace.sql。

    b.  运行`Set @durationInMins=0` ，以便跟踪捕获不会在指定的时间后自动停止。

    c.  若要设置每个跟踪文件的最大文件`Set @maxfilesize`大小，请运行。 建议的大小为200（以 MB 为单位）。

    d.单击“下一步”。  编辑`@Tracefile`以为跟踪文件设置唯一名称。

    e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。  如果`@dbname`只能在特定数据库上捕获工作负荷，请编辑以指定数据库名称。 默认情况下，将捕获整个服务器上的工作负荷。

4. 若要针对目标 SQL Server 实例重播 IRF 文件，请在命令提示符下运行以下命令：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  若要监视状态，请在命令提示符下运行`DReplay status -f 1`。

    b.  若要停止重播，例如，如果在命令提示符处看到 pass% 低于预期，请运行`DReplay cancel`。

5. 停止目标 SQL Server 实例上的跟踪捕获。
6. 在 SSMS 中打开`<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`。
7. 编辑`@Tracefile`此项可匹配运行 SQL Server 的目标计算机上的跟踪文件路径。
8. 针对运行 SQL Server 的目标计算机运行脚本。

## <a name="analyze-traces-using-the-dea-command"></a>使用 DEA 命令分析跟踪

若要启动新的跟踪分析，请在命令提示符下运行以下命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**示例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>另请参阅

- 有关使用 DEA 的详细信息，请参阅[数据库实验助手概述](database-experimentation-assistant-overview.md)。
