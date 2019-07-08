---
title: 获取完整内存转储来排查 SQL Server Management Studio (SSMS) 问题
Description: 通过收集完整内存转储来排查 SSMS 挂起或故障问题
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: dineth, sstein
ms.custom: ''
ms.date: 05/17/2019
ms.openlocfilehash: af7f9222a5de8c0e899d22d32e53d7638a4158cb
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412894"
---
# <a name="get-full-memory-dump"></a>获取完整内存转储

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

本文将介绍如何捕获诊断信息来排查 SQL Server Management Studio (SSMS) 故障或挂起问题。

若要捕获诊断信息来排除故障，请按照以下步骤操作。

1. 下载 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 将下载内容解压缩到文件夹中。

3. 打开命令提示符（如 `cmd.exe`），并运行以下命令。

    ```
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    它应该会提示你接受许可协议，请选择“同意”  。

4. 启动 SQL Server Management Studio (SSMS)（如果尚未启动的话）。

5. 重现遇到的问题。

6. 关于写入转储文件的命令提示符中应该会出现文本，请等待此操作完成。

7. 新建文件夹，并将写入操作输出的 *.dmp 文件复制此文件夹中。

8. 将下列文件复制到同一文件夹中。

    * “C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll”
    * “C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll”
    * “C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll”

9. 压缩此文件夹。

## <a name="outofmemoryexception"></a>OutOfMemoryException

还可以在 SSMS 抛出 OutOfMemoryException（可以是任意托管异常）时获取 SSMS 的完整内存转储。

若要捕获诊断信息来排查 SSMS 抛出的 OutOfMemoryException，请按照以下步骤操作。

1. 下载 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 将下载内容解压缩到文件夹中。

3. 打开命令提示符，并运行以下命令。

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    它应该会提示你接受许可协议，请选择“同意”  。

4. 启动 SQL Server Management Studio（如果尚未启动的话）。

5. 重现遇到的问题。

6. 关于写入转储文件的命令提示符中应该会出现文本，请等待此操作完成。

7. 新建文件夹，并将写入操作输出的 *.dmp 文件复制此文件夹中。

8. 将下列文件复制到同一文件夹中。

    * “C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll”
    * “C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll”
    * “C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll”

9. 压缩此文件夹。

## <a name="share-the-information"></a>共享信息

1. 若要与 SSMS 团队共享信息，请在 https://aka.ms/sqlfeedback 处记录问题。

2. 然后将收集的内存转储文件共享到可以收集文件的 OneDrive（或等效位置）。

    > [!Important]
    > 内存转储文件可能包含敏感信息。

## <a name="next-steps"></a>后续步骤

[SQL Server Management Studio](../sql-server-management-studio-ssms.md)