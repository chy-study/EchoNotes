---
title: Delphi 笔记
---

- AssignFile(F, 'C:\MyFile.txt')
   - 将C:\MyFile.txt文件与F变量建立连接，后面可以使用答F变量对文件进行操作。
- Rewrite（）
   - 创建不存在的文件但不包括文件夹
- ReadSections
   - 读取ini文件里面[]的值
- ReadSectionValues
   - 读取ini文件[]下面的key-value值
- readstring("小节名","关键字",缺省值)
   - 指定读取ini文件[]下面key对应的value值
- EOF
   - 是一个计算机术语，为End Of File的缩写，在操作系统中表示资料源无更多的资料可读取
- ShowWindowAsync
   - 一种函数，功能是该函数设置由不同线程产生的窗口的显示状态。
- ComponentCount
   - 指打开的窗体所拥有的控件个数，包含所有子组件、孙组件(子组件内的子组件)
- interval
   - 单位是0.001秒.如果该属性设置为1000,就是每隔一秒执行下OnTimer程序
- SetWindowLong  是一个WindowsAPI函数。该函数用来改变指定窗口的属性．函数也将指定的一个32位值设置在窗口的额外存储空间的指定偏移位置。
	```
	函数原型：
	LONG SetWindowLong(
	    HWND hWnd,               // handle to window
	    int nlndex,              // offset of value to set
	    LONG dwNewLong           // new value
	);
	如果函数成功，返回值是指定的32位整数的原来的值。如果函数失败，返回值为0。若想获得更多错误信息，请调用GetLastError函数。
	```
- 患者表：HOKUDAI1.B_PATIENT_INFO
- Imemode属性：
   - imClose 表示输入法处于关闭状态；
   - ImOpen 表示输入法处于打开状态；
   - ImChinese 表示处于中文输入法状态；
   - ImDontCare 表示若输入法处于关闭状态则打开最近一次使用过的输入法；
   - ImSAlpha 表示输入处于半角状态；
   - ImAlpha 表示输入处于全角状态。
- OnNeedData:
   - 这个事件本身是一个循环，循环起点是把MoreData置为真 “MoreData:=True;”
	紧接着要注意加入判定是否结束语句
	如：if QRDBText1.Dataset.Eof then MoreData:=False;
	如果判断语句放在事件最后，将导致QRDBText1.Dataset的最后一条记录不会被打印。
	该事件非常适合用于在追加数据集时根据数据集的内容设置字体等
- FindFirst：
   - 是用来寻找目标目录下的第一个文件，当成功找到文件时,返回0.
- FindNext：
   - 则是寻找下一个
- Rewrite(<文件变量名>)：
   - 若无该文件，则创建文件。
	若有该文件，覆盖掉原文件。
	打开文件后，可以对文件内容进行写操作。

- Append(<文件变量名>)：
   - 追加内容到文件中。文件必须要存在。

- application.ProcessMessages:
   - 主要作用使程序在循环时能够响应外界事件。一般情况下，程序在循环的时候不响应外界事件。直到循环结束为止才能接受和响应外界事件。application.ProcessMessages可以有效的解决循环循环的独占问题，能够暂时中断应用程序的执行
- IncludeTrailingPathDelimiter(const S:String):String
   - 和IncludeTrailingBackslash是同样功能，不过根据delphi的帮助，我们现在应该使用IncludeTrailingPathDelimiter才对，前者只是为了向前兼容才保留的,这个函数是将参数S提供的一个表示路径的末尾加上“/”符（如果是unix系统，则加上“/”）
- ExcludeTrailingPathDelimiter(const S:String):String
   - 和ExcludeTrailingBackslash是同样功能，同样我们应该使用ExcludeTrailingPathDelimiter
这个函数和IncludeTrailingPathDelimiter正好相反，是用来去掉一个路径末尾的斜杠符的
- 拷贝参考的文件后，需要提交一次原始的代码，注释是copy...
- 打印：
   - 先安装驱动（LBP3018_R150_V110_W32_ZH_1.exe这个EXE解压后里面有setup），再连接打印机地址 双击连接打印机地址时出来的打印机图标
   - 打印机地址 192.168.15.125
   - user:administrator
   - password:newtouch@1234125
- 表：
   - I_Results_view 检查结果登录表
   - D_RECORD 透析记录表
   - B_PATIENT_INFO 患者信息表