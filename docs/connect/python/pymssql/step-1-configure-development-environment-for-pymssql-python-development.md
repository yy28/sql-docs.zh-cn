---
title: '步骤 1: 配置 pymssql Python 开发环境 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bf2942b79cf7e72efbb36a53019de8208cd3b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935829"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>步骤 1：配置用于 pymssql Python 开发的开发环境
需要使用系统必备组件配置开发环境, 以便使用 Python Driver for SQL Server 开发应用程序。    
  
请注意, Python SQL 驱动程序使用 TDS 协议, 该协议默认情况下在 SQL Server 和 Azure SQL 数据库中启用。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 Python 运行时和 pip 包管理器**  
A. 中转到[python.org](https://www.python.org/downloads/)  
B. 单击相应的 "Windows installer msi" 链接。   
c. 下载后, 运行 msi 以安装 Python 运行时  
  
2. 从[此处](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)**下载 pymssql 模块**  
  
    请确保选择正确的 whl 文件。  例如: 如果在64位计算机上使用 Python 2.7, 请选择: pymssql-2.1.1-cp27-none-win_amd64. whl。 下载 whl 文件后, 将其放在 C:/Python27 文件夹中。  
      
3. **打开 cmd.exe**  
  
4. **安装 pymssql 模块**     
    例如, 如果在64位计算机上使用 Python 2.7:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **安装 Python 运行时和 pip 包管理器** 在大多数 Ubuntu 分发版上预安装了 Python。  如果你的计算机未安装 python, 则可以从[python.org](https://www.python.org/downloads/)下载源 tarball 并在本地生成, 也可以使用包管理器:  
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
  
## <a name="mac"></a>Mac  
  
1. **安装 Python 运行时和 pip 包管理器**  
A. 中转到[python.org](https://www.python.org/downloads/)  
B. 单击相应的 Mac 安装程序 .pkg 链接。   
c. 下载完成后, 运行 .pkg 以安装 Python 运行时  
  
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
