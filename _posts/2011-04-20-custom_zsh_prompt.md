--- 
title: "定制你的 zsh 命令提示符"
category: ["Linux"]
tags: ["zsh", "命令提示符"]
---

官方文档地址：<a href="http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html">http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html</a>

我自己的命令提示符

```bash
PROMPT='%B%{[32m%}%n%(?. . %{[31m%}%? )%{[m%}> %{[1;34m%}%~ %{[m%}%# %b'
```

再把翻译的文章贴出来，文中有一部分可能没有翻译，那个也请见谅&hellip;&hellip;

<article>
<h2>有关提示符的色彩</h2>

zsh里着色需要在转义字符/普通字符前填入：

```bash
%{^[[<色彩编号>m%}</pre>
```

其中 `^[` 需要 Vim 在插入模式下按下 <kbd>Ctrl+v</kbd> <kbd>Esc</kbd> 才能输入，如果没有输入色彩的编号，那么就是默认色彩

色彩编号如下：

<table>
<tr><td>Black 0;30</td><td>Dark Gray 1;30</td></tr>
<tr><td>Blue 0;34</td><td>Light Blue 1;34</td></tr>
<tr><td>Green 0;32</td><td>Light Green 1;32</td></tr>
<tr><td>Cyan 0;36</td><td>Light Cyan 1;36</td></tr>
<tr><td>Red 0;31</td><td>Light Red 1;31</td></tr>
<tr><td>Purple 0;35</td><td>Light Purple 1;35</td></tr>
<tr><td>Brown 0;33</td><td>Yellow 1;33</td></tr>
<tr><td>Light Gray 1;37</td><td>White 1;37</td></tr>
</table>

<h2>提示符介绍</h2>

</h4>Special characters</h4>
<table>
<tr><td>%%</td><td>一个'%'</td></tr>
<tr><td>#%)</td><td>一个')'</td></tr>
</table>

<h4>Login information</h4>
<table>
<tr><td>%y</td><td>当前的tty名</td></tr>
<tr><td>%l</td><td>当前的tty名，如 pts/1 </td></tr>
<tr><td>%M</td><td>完整主机名</td></tr>
<tr><td>%m</td><td>主机名（在第一个句号之前截断）</td></tr>
<tr><td>%n</td><td>当前用户名</td></tr>
</table>

<h4>Shell state</h4>
<table>
<tr><td>%. %c %C</td><td> 前两个显示相对路径的当前文件夹名，最后一个是绝对路径（也就是说，前两个在家目录下显示'~'，最后那个显示你的用户名），'%'后的数字表示显示几层路径</td></tr>
<tr><td>%N</td><td>zsh 正在执行的脚本/函数名。如果'%'后跟了数字，似乎还有其他作用</td></tr>
<tr><td>%L</td><td>当前shell的层数，可以参考《盗梦空间》的层数</td></tr>
<tr><td>%j</td><td>当前正在进行的工作数量</td></tr>
<tr><td>%i</td><td>与%!类似：The line number currently being executed in the script, sourced file, or shell function given by %N. This is most useful for debugging as part of $PS4.</td></tr>
<tr><td>%!</td><td>显示当前历史事件号码（也就是打开shell后第几条命令）</td></tr>
<tr><td>%/ %d</td><td>显示当前工作路径（$pwd）。如果'％'后面是一个整数，它指定显示路径的元件的数量;没有数字就显示整个路径。一个负整数就是指定主目录，即％-1d代表第一部分</td></tr>
<tr><td>%~</td><td>目前的工作目录相对于～的相对路径</td></tr>
<tr><td>`%_`</td><td>The status of the parser, i.e. the shell constructs (like `if` and `for`) that have been started on the command line. If given an integer number that many strings will be printed; zero or negative or no integer means print as many as there are. This is most useful in prompts PS2 for continuation lines and PS4 for debugging with the XTRACE option; in the latter case it will also work non-interactively.</td></tr>
<tr><td>%?</td><td>返回最后命令的执行结果的代码</td></tr>
<tr><td>%#</td><td>用户组，#（普通用户）/%（超级用户）</td></tr>
</table>

<h4>Date and time</h4>
<table>
<tr><td>%D{}</td><td>格式化日期，内容在下：<br />
  %f %e ：当月日期 (如果是个位数的话，第二个比第一个多一个占位符（一个空格）<br />
  %K %k ：24小时制，第二个比第一个多占位符<br />
  %L %l ：12小时制，第二个比第一个多占位符</td></tr>
<tr><td>%W</td><td>系统日期 (月-日-年)</td></tr>
<tr><td>%w</td><td>系统日期 (周几 日期)</td></tr>
<tr><td>%D</td><td>系统日期（年-月-日）</td></tr>
<tr><td>%T</td><td>系统时间（时：分），24小时制</td></tr>
<tr><td>%t %@</td><td>系统时间，12小时制</td></tr>
<tr><td>`%*`</td><td>系统时间（时：分：秒）</td></tr>
</table>

<h4>Visual effects</h4>
<table>
<tr><td>%B(%b)</td><td>开始到结束使用粗体打印</td></tr>
<tr><td>%U(%u)</td><td>开始到结束使用下划线打印</td></tr>
<tr><td>%S(%s)</td><td>开始到结束使用突出模式打印</td></tr>
<tr><td>%{..%}</td><td>可以输入一些转义字符，花括号里的内容不会改变光标位置，花括号可以嵌套</td></tr>
<tr><td>%E</td><td>清空一行</td></tr>
</table>

<h4>Conditional substrings</h4>
%v ：获取 psvar 数组的第一个值，&rsquo;%&lsquo;后是什么数字就返回第几个值，负数就返回倒数过去的值
%(x.true-text.false-text) ：
这是一个判断式，判断 x 的真假，真则输出 true-text ，否则输出 false-text
左侧括号前后可以插入一个正数n，如果是负数的话就会被乘以 -1，n在下文会用到
x 有以下内容：
<table>
<tr><td> ! </td><td>是否是root权限</td></tr>
<tr><td> # </td><td>当前进程的UID是否等于n</td></tr>
<tr><td> g </td><td>当前进程的有效GID是否等于n</td></tr>
<tr><td> ? </td><td>最后命令的返回值是否等于n</td></tr>
<tr><td> _ </td><td>当前是否有至少n个shell constructs正在执行</td></tr>
<tr><td> C / </td><td>当前的绝对路径是否至少有n个元素</td></tr>
<tr><td> c . ~ </td><td>当前路径距离根目录(/)是否至少有n个元素，/算是0 </td></tr>
<tr><td> D </td><td>当前月份是否等于n，1月等于0</td></tr>
<tr><td> d </td><td>当前日期是否等于n</td></tr>
<tr><td> j </td><td>当前作业数是否等于n</td></tr>
<tr><td> L </td><td>当前shell层数是否等于n</td></tr>
<tr><td> l </td><td>当前是否已经至少有n个字符已经打印</td></tr>
<tr><td> S </td><td>当前的秒数是否至少为n</td></tr>
<tr><td> T </td><td>当前小时是否等于n</td></tr>
<tr><td> t </td><td>当前的分钟是否等于n</td></tr>
<tr><td> v </td><td>当前 psvar 数组是否已经至少有n个元素</td></tr>
<tr><td> w </td><td>是否等于周n，周日是0</td></tr>
</table>

> %<string<  
> %>string>  
> %[xstring]  
> Specifies truncation behaviour for the remainder of the prompt string. The `>'. The numeric argument, which in the third form may appear immediately after the `[', specifies the maximum permitted length of the various strings that can be displayed in the prompt. The string will be displayed in place of the truncated portion of any string; note this does not undergo prompt expansion.

> The forms with `<' truncate at the left of the string, and the forms with `>' truncate at the right of the string. For example, if the current directory is `/home/pike', the prompt `%8<..<%/' will expand to `..e/pike'. In this string, the terminating character (`<', `>' or `]'), or in fact any character, may be quoted by a preceding `\'; note when using print -P, however, that this must be doubled as the string is also subject to standard print processing, in addition to any backslashes removed by a double quoted string: the worst case is therefore `print -P "%<\\\\<<..."'.

> If the string is longer than the specified truncation length, it will appear in full, completely replacing the truncated string.

> The part of the prompt string to be truncated runs to the end of the string, or to the end of the next enclosing group of the `%(' construct, or to the next truncation encountered at the same grouping level (i.e. truncations inside a `%(' are separate), which ever comes first. In particular, a truncation with argument zero (e.g. `%<<') marks the end of the range of the string to be truncated while turning off truncation from there on. For example, the prompt '%10<...<%~%<<%# ' will print a truncated representation of the current directory, followed by a `%' or `#', followed by a space. Without the `%<<', those two characters would be included in the string to be truncated.

</article>
