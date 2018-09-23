小型文本处理器的建立
===
   该作业由C/C++语言构建，由于非计算机相关专业，代码若有不够规范的地方请指正，谢谢！<br>
   该作业为第二次提交的作业，主要修改为将结构体str成员变为字符向量vector<char>，change函数中也将原来字符数组改为字符向量，这样便捷很多且空间利用率提高，其中两个字符向量的拼接和字符向量和字符数组的拼接参考stackoverflow上代码。
## 1.创建结构体Word
    该结构体有两个成员：str和row
    ***其中str为变长字符向量，用于存放分割后的单词或者空格
    row为整型集合，记录该单词所在行数，由于集合自动去重并排序，用于记录行数较为方便
## 2.全局变量
    wordNum-表示单词计数；charNum-表示合法字符计数器，用于分行；rowNum-用于记录行数；flag用于判断文本字符和排版宽度是否合法 
## 3.函数change
    函数返回值：返回值类型为字符向量，即更改后的文本
    形参: 需要转换的文本text，int型排版宽度width 
    函数体：
          1.先求出字符串长度，代码27-45行检验是否有非法字符或者宽度不满足要求，有就返回ERROR
          2.作业中示例未有首行首个单词即为空格的文本，代码48-66行处理首行首个单词为空格的情况；
            67行:
            else if(text[i]!=' ')是对非空字符的处理
            75行:
	        else if(text[i] == ' ')对其他空字符处理
          3.对行号的处理
            56行:
            rowNum = ((charNum-1)/width+1);
            是对该单词所在行数的处理,rowNum为该单词所在行数
		例如排版宽度为10，当前是第10个合法字符，rowNum = (10-1)/10+1 = 1；即该单词在第一行
            57行:
            word[wordNum].row.insert(rowNum);
            在该单词的row集合中插入该行数，若已有则自动去重并排序
          4.对非空字符和其余空字符的处理
            59-63行:
            若空字符结束，则令新单词数量+1，终结本层循环
            67行：
            处理非空字符的单词，和处理空字符基本一样
            75行：
            对其他空字符处理，若从空字符到非空字符，新单词+1
          5.将word结构体数组中每个单词拼接到新字符向量newStr中
	    ***其中两个字符向量的拼接来自https://stackoverflow.com/questions/2551775/appending-a-vector-to-a-vector
            其中strSub为单词后字符（行号，行号***）的处理，countDot记录逗号的数量
            105行对集合的for循环：
            依次遍历各个单词的行号 ，并将整型行号转为字符串格式拼接到strSub后面
          6.函数最后将newStr和strSub拼接在一起
	    ***字符newStr和字符数组的拼接来自https://stackoverflow.com/questions/1399666/attaching-char-buffer-to-vectorchar-in-stl
 ## 4.main函数
    对输入的文本动态分配内存，经change函数处理后返回给newStr，并输出，最后释放动态分配内存空间
 ## 5.运行
    直接运行HomeWorkChanged.cpp文件，按照提示输入参数及文本即可
