---
title: 不受支持的 Visual FoxPro 命令和函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e5b8ed06ad9f996d644df0dfb99d15adcff86bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307648"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>不支持的 Visual FoxPro 命令和函数（Visual FoxPro ODBC 驱动程序）
下表列出了 Visual FoxPro ODBC 驱动程序不支持的 FoxPro 命令和函数，但受 Microsoft® Visual FoxPro®支持。  
  
 如果您的应用程序与其规则、触发器、默认值或存储过程调用这些 Visual FoxPro 命令或函数的数据交互，则驱动程序将生成错误。  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>不受支持的 Visual FoxPro 命令和函数  
  
||||  
|-|-|-|  
|#DEFINE ... #UNDEF|#IF ... #ENDIF 预处理器指令|#IFDEF &#124; #IFNDEF|  
|#INCLUDE 预处理器指令|：：作用域解析运算符|! 命令（请参阅 RUN &#124;！ Command|  
|? &#124;？ 命令|??? 命令|\ &#124; \\\ 命令|  
|@ ...BOX 命令|@ ...CLASS 命令|@ ...清除命令|  
|@ ...编辑-编辑框命令|@ ...FILL 命令|@ ...获取|  
|@ ...菜单命令|@ ...PROMPT 命令|@ ...说命令|  
|@ ...SCROLL 命令|@ ...TO 命令||  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ACCEPT 命令|ACLASS （）函数|"激活" 菜单命令|  
|激活 POPUP 命令|激活屏幕命令|激活窗口命令|  
|ActivateCell 方法|添加类命令|ADIR （）函数|  
|AFONT （）函数|AINSTANCE （）函数|_ALIGNMENT 系统内存变量|  
|AMEMBERS （）函数|ANSITOOEM （）函数|APRINTERS （）函数|  
|ASELOBJ （）函数|帮助命令||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BAR （）函数|BARCOUNT （）函数|BARPROMPT （）函数|  
|_BEAUTIFY 系统内存变量|_BOX 系统内存变量|浏览命令|  
|_BROWSER 系统内存变量|生成应用命令|BUILD EXE 命令|  
|"生成项目" 命令|_BUILDER 系统内存变量||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|_CALCVALUE 系统内存变量|_CLIPTEXT 系统内存变量|_CONVERTER 系统内存变量|  
|_CUROBJ 系统内存变量|CALL 命令|取消命令|  
|CAPSLOCK （）函数|CD 命令|CHANGE 命令|  
|CHDIR 命令|CHRSAW （）函数|关闭 MEMO 命令|  
|CNTBAR （）函数|CNTPAD （）函数|COL （）函数|  
|编译命令|COMPILE 数据库命令|编译窗体命令|  
|COMPOBJ （）函数|容器对象|Control 对象|  
|"复制文件" 命令|复制备注命令|CREATE CLASS 命令|  
|CREATE CLASSLIB 命令|"创建颜色集" 命令|CREATE 命令|  
|创建连接命令|CREATE DATABASE 命令|创建窗体命令|  
|从命令创建|创建标签命令|CREATE MENU 命令|  
|创建项目命令|CREATE QUERY 命令|创建报表命令|  
|创建屏幕命令|创建 SQL 视图命令|CREATE TRIGGER 命令|  
|创建视图命令|CREATEOBJECT （）函数|CURDIR （）函数|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK 系统内存变量|_DIARYDATE 系统内存变量|DBSETPROP （）函数|  
|DDE 函数|停用菜单命令|停用弹出命令|  
|停用窗口命令|DECLARE DLL 命令|DECLARE 命令|  
|定义 BAR 命令|定义 BOX 命令|DEFINE CLASS 命令|  
|定义菜单命令|定义填充命令|定义 POPUP 命令|  
|定义窗口命令|删除连接命令|删除数据库命令|  
|删除文件命令|DELETE TRIGGER 命令|删除视图命令|  
|DIR 命令|DIRECTORY 命令|显示命令|  
|显示连接命令|显示数据库命令|显示 DLL 命令|  
|显示文件命令|显示内存命令|显示对象命令|  
|显示过程命令|显示状态命令|显示结构命令|  
|显示表命令|显示视图命令|DO 窗体命令|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|编辑命令|ERROR 命令||  
|ERASE 命令|外部命令|导出命令|  
|弹出命令|弹出页面命令||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC 系统内存变量|_FOXGRAPH 系统内存变量|FEOF （）函数|  
|FCLOSE （）函数|FCREATE （）函数|FGETS （）函数|  
|FERROR （）函数|FFLUSH （）函数|FKLABEL （）函数|  
|文件服务器命令|FIND 命令|FOPEN （）函数|  
|FKMAX （）函数|FONTMETRIC （）函数|FSEEK （）函数|  
|FPUTS （）函数|FREAD （）函数||  
|FWRITE （）函数|FCHSIZE （）函数||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH 系统内存变量|_GENMENU 系统内存变量|_GENPD 系统内存变量|  
|_GENSCRN 系统内存变量|_GENXTAB 系统内存变量|GETBAR （）函数|  
|GETCOLOR （）函数|GETDIR （）函数|GETEXPR 命令|  
|GETFILE （）函数|IVSFONTANDCOLORSTORAGE.GETFONT 错误（）函数|GETOBJECT （）函数|  
|GETPAD （）函数|GETPICT （）函数|GETPRINTER （）函数|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|HELP 命令|隐藏菜单命令|隐藏 POPUP 命令|  
|隐藏窗口命令|HOME （）函数||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS （）函数|导入命令|输入命令|  
|命令索引|INKEY （）函数|ISCOLOR （）函数|  
|插入命令|INSMODE （）函数||  
|ISMOUSE （）函数|_INDENT 系统内存变量||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|JOIN 命令|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|键盘命令|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN 系统内存变量|标签命令|LASTKEY （）函数|  
|LINENO （）函数|列出命令|列出连接命令|  
|LOAD 命令|LOCFILE （）函数||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL （）函数|MD 命令|命令菜单|  
|MEMORY （）函数|菜单命令|MKDIR 命令|  
|MENU （）函数|MESSAGEBOX （）函数|修改连接命令|  
|MODIFY CLASS 命令|修改命令命令|修改窗体命令|  
|修改数据库命令|修改文件命令|修改 MEMO 命令|  
|修改常规命令|修改标签命令|修改项目命令|  
|修改菜单命令|MODIFY PROCEDURE 命令|修改屏幕命令|  
|修改查询命令|修改报表命令|修改窗口命令|  
|修改结构命令|修改视图命令|移动窗口命令|  
|鼠标命令|移动 POPUP 命令|MROW （）函数|  
|MRKBAR （）函数|MRKPAD （）函数||  
|MWINDOW （）函数|MDOWN （）函数||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUMLOCK （）函数|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM （）函数|OBJTOCLIENT （）函数|ON BAR 命令|  
|OEMTOANSI （）函数|ON APLABOUT 命令|退出菜单命令|  
|ON ESCAPE 命令|ON EXIT BAR 命令|ON KEY = 命令|  
|ON EXIT PAD 命令|退出时弹出命令|ON PAD 命令|  
|键标签命令|ON MACHELP 命令|选择条命令|  
|页面命令|ON READERROR 命令|在选定内容弹出命令上|  
|"选择时" 菜单命令|在选择板上的命令||  
|关闭时命令|OBJVAR （）函数||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE 系统内存变量|_PAGENO 系统内存变量|_PBPAGE 系统内存变量|  
|_PCOLNO 系统内存变量|_PCOPIES 系统内存变量|_PDRIVER 系统内存变量|  
|_PDSETUP 系统内存变量|_PECODE 系统内存变量|_PEJECT 系统内存变量|  
|_PEPAGE 系统内存变量|_PLENGTH 系统内存变量|_PLINENO 系统内存变量|  
|_PLOFFSET 系统内存变量|_PPITCH 系统内存变量|_PQUALITY 系统内存变量|  
|_PRETEXT 系统内存变量|_PSCODE 系统内存变量|_PSPACING 系统内存变量|  
|_PWAIT 系统内存变量|PACK 数据库命令|PAD （）函数|  
|PCOL （）函数|PEMSTATUS （）函数|播放宏命令|  
|POP 键命令|POP 菜单命令|弹出菜单命令|  
|POPUP （）函数|PRINTJOB ...ENDPRINTJOB 命令|PRINTSTATUS （）函数|  
|PRMBAR （）函数|PRMPAD （）函数|PROMPT （）函数|  
|PROW （）函数|PRTINFO （）函数|推送键命令|  
|推送菜单命令|推送 POPUP 命令|PUTFILE （）函数|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|退出命令|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN 系统内存变量|RD 命令|READKEY （）函数|  
|READ 命令|读取菜单命令|RELEASE BAR 命令|  
|REFRESH （）函数|重新索引命令|RELEASE LIBRARY 命令|  
|RELEASE CLASSLIB 命令|RELEASE 命令|RELEASE PAD 命令|  
|RELEASE 菜单命令|RELEASE MODULE 命令|RELEASE WINDOWS 命令|  
|释放弹出命令|RELEASE PROCEDURE 命令|重命名命令|  
|删除类命令|RENAME CLASS 命令|重命名视图命令|  
|RENAME 连接命令|RENAME TABLE 命令|从命令还原|  
|报表命令|REQUERY （）函数|还原窗口命令|  
|还原宏命令|还原屏幕命令|RGBSCHEME （）函数|  
|RESUME 命令|RGB （）函数|运行 &#124;！ 命令|  
|RMDIR 命令|ROW （）函数||  
|RUNSCRIPT 命令|RDLEVEL （）函数||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|保存宏命令|保存屏幕命令|保存到命令|  
|保存 WINDOWS 命令|图式（）函数|SCOLS （）函数|  
|SCROLL 命令|_SCREEN 系统内存变量|SET 命令|  
|设置替换命令|SET ANSI 命令|SET APLABOUT 命令|  
|设置自动保存命令|设置电铃命令|设置闪烁命令|  
|设置边框命令|SET BRSTATUS 命令|SET CLASSLIB 命令|  
|设置清除命令|设置时钟命令|设置命令颜色|  
|设置方案命令的颜色|设置颜色集命令|将颜色设置为命令|  
|设置兼容的命令|设置 CONFIRM 命令|设置控制台命令|  
|设置 CPCOMPILE|设置 CPDIALOG|设置货币命令|  
|设置 CURSOR 命令|SET DATASESSION 命令|设置调试命令|  
|"设置小数" 命令|设置分隔符命令|设置开发命令|  
|设置设备命令|设置显示命令|SET DOHISTORY 命令|  
|设置 ECHO 命令|设置转义命令|设置格式命令|  
|设置函数命令|设置标题命令|设置帮助命令|  
|SET HELPFILTER 命令|设置强度命令|设置键命令|  
|SET KEYCOMP 命令|SET LOGERRORS 命令|SET MACDESKTOP 命令|  
|SET MACHELP 命令|SET MACKEY 命令|设置边距命令|  
|设置命令标记|将 "标记" 设置为命令|SET MEMOWIDTH 命令|  
|设置消息命令|设置鼠标命令|SET 里程表读数命令|  
|SET OLEOBJECT 命令|设置调色板命令|SET PDSETUP 命令|  
|设置点命令|设置打印机命令|SET READBORDER 命令|  
|设置刷新命令|设置资源命令|设置安全命令|  
|设置记分板命令|设置秒数命令|设置分隔符命令|  
|设置 SHADOWS 命令|设置命令跳过|设置空间命令|  
|设置状态命令|设置状态栏命令|设置步骤命令|  
|设置粘滞命令|SET SYSFORMATS 命令|SET SYSMENU 命令|  
|设置谈话命令|SET TEXTMERGE 命令|设置 TEXTMERGE 分隔符命令|  
|设置主题命令|设置主题 ID 命令|SET TRBETWEEN 命令|  
|SET TYPEAHEAD 命令|设置视图命令|设置 MEMO 命令窗口|  
|SET XCMDFILE 命令|_SHELL 系统内存变量|显示 GET 命令|  
|SHOW 获取命令|显示菜单命令|显示对象命令|  
|显示弹出项命令|显示窗口命令|SIZE POPUP 命令|  
|大小窗口命令|SKPBAR （）函数|SKPPAD （）函数|  
|SOUNDEX （）函数|_SPELLCHK 系统内存变量|SQL 函数|  
|SROWS （）函数|_STARTUP 系统内存变量|挂起命令|  
|Sys （）函数（SYS （2011）除外）|SYSMETRIC （）函数||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS 系统内存变量|文本 .。。ENDTEXT 命令|TXTWIDTH （）函数|  
|TRANSFORM （）函数|_TRANSPORT 系统内存变量||  
|TYPE 命令|_THROTTLE 系统内存变量||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UPDATED （）函数|USE 命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VALIDATE 数据库命令|VARREAD （）函数|VERSION （）函数|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|_WINDOWS 系统内存变量|_WIZARD 系统内存变量|WCHILD （）函数|  
|等待命令|WBORDER （）函数|WFONT （）函数|  
|WCOLS （）函数|WEXIST （）函数|WLROW （）函数|  
|用 .。。ENDWITH 命令|WLAST （）函数|WONTOP （）函数|  
|WMAXIMUM （）函数|WLCOL （）函数|WREAD （）函数|  
|WOUTPUT （）函数|WMINIMUM （）函数|WVISIBLE （）函数|  
|WPARENT （）函数|WTITLE （）函数||  
|WROWS （）函数|_WRAP 系统内存变量||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZOOM 窗口命令|||
