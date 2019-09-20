---
title: SQL Server Management Studio (SSMS) 挂起或崩溃故障排除
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: e73e3d8cc0b54f0251530327dbcea941546471d5
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212436"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>在 SQL Server Management Studio (SSMS) 崩溃后，获取诊断数据

[!INCLUDE[适用范围](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>挂起或故障后获取完整内存转储

在 SQL Server Management Studio (SSMS) 挂起或故障后，获取它的完整内存转储。

若要捕获诊断信息来排除 SSMS 崩溃或挂起故障，请按照以下步骤操作。

1. 下载 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 将下载内容解压缩到文件夹中。

3. 打开命令提示符，并运行以下命令。

    ```console
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    提示你接受许可协议时，请选择“同意”  。

4. 如果尚未启动 SSMS，请启动它。

5. 重现问题。

6. 关于写入转储文件的命令提示符中应该会出现文本，请等待此操作完成。

7. 新建文件夹，并将写入操作输出的 *.dmp 文件复制此文件夹中。

8. 将下列文件复制到同一文件夹中。

    “C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll”  “C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll”  “C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll”

9. 压缩此文件夹

## <a name="get-full-memory-dump-for-an-outofmemoryexception"></a>获取 OutOfMemoryException 的完整内存转储

当 SSMS 引发 OutOfMemoryException 时，获取它的完整内存转储。

可获取任何托管异常的完整内存转储。

若要捕获诊断信息以排查 SSMS 引发的 OutOfMemoryException，请按照以下步骤操作。

1. 下载 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 将下载内容解压缩到文件夹中。

3. 打开命令提示符，并运行以下命令。

    ```console
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    提示你接受许可协议时，请选择“同意”  。

4. 启动 SQL Server Management Studio（如果尚未启动的话）。

5. 重现问题。

6. 关于写入转储文件的命令提示符中应该会出现文本，请等待此操作完成。

7. 新建文件夹，并将写入操作输出的 *.dmp 文件复制此文件夹中。

8. 将下列文件复制到同一文件夹中。

    “C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll”  “C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll”  “C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll”

9. 压缩此文件夹。
