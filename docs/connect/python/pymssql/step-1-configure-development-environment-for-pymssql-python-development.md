---
title: 步骤 1：配置 pymssql 环境
description: 本入门指南的第 1 步涉及在开发环境中安装 Python、Microsoft ODBC Driver for SQL Server 和 pymssql。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5eb4a746cf8847c8300091677fe4e07e8173707
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634614"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>步骤 1：配置用于 pymssql Python 开发的开发环境
需要配置满足先决条件的开发环境，才能使用 Python Driver for SQL Server 开发应用程序。    
  
Python SQL 驱动程序使用 TDS 协议，此协议在 SQL Server 和 Azure SQL 数据库中默认启用。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. 安装 Python 运行时和 pip 包管理器。   
a. 转到 [python.org](https://www.python.org/downloads/)  
b. 单击相应的 Windows 安装程序 msi 链接。   
c. 下载后，运行 msi 以安装 Python 运行时  
  
2. 从[此处](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)下载 pymssql 模块   
  
    请确保选择了正确的 `whl` 文件。  例如：若要在 64 位计算机上使用 Python 2.7，请选择“`pymssql‑2.1.1‑cp27‑none‑win_amd64.whl`”。 下载 `whl` 文件后，将它放入 C:\Python27 文件夹。  
      
3. **打开 cmd.exe**  
  
4. 安装 pymssql 模块。   
    例如，若要在 64 位计算机上使用 Python 2.7：  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. 安装 Python 运行时和 pip 包管理器。   Python 预安装在大多数 Ubuntu 发行版本中。  如果计算机中未安装 python，可以从 [python.org](https://www.python.org/downloads/) 下载源 Tarball 并在本地生成，也可以使用包管理器：  
```  
> sudo apt-get install python   
```  
  
2.  **打开终端**  
  
3.  **安装 pymssql 模块和依赖项**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="macos"></a>macOS
  
1. **安装 Python 运行时和 pip 包管理器**  
a. 转到 [python.org](https://www.python.org/downloads/)  
b. 单击相应的 macOS 安装程序 pkg 链接。   
c. 下载完成后，运行 pkg 以安装 Python 运行时  
  
2.  **打开终端**  
  
3. **安装 Homebrew 包管理器**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **安装 FreeTDS 模块**  
```  
> brew install FreeTDS  
```  
  
5.  **安装 pymssql 模块**  
```  
> sudo -H pip install pymssql  
```
