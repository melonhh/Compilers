# 编译原理
## 引论
### 编译程序
1. 计算机的CPU只能执行目标程序（什么是目标程序，为什么只能执行目标程序）
2. 编译程序将程序设计语言书写的源程序翻译为与其等价的目标程序
3. 处理过程
   1. 从源程序中读入字符流，识别出单词流
   2. 确定单词流在语法上是否正确（用语法树表示）
   3. 语义分析（例如变量类型审查，对实数数组下标的情况进行检查）
   4. 中间代码生成（将源程序变成一种内部表示，称为中间代码）
   5. 代码优化
   6. 目标代码生成

### 编译程序的结构
1. 组成
   1. 单词是语言中具有独立意义的最小语法单位
   2. 属性字是单词的一种机内表示（长度统一，刻画了单词的属性）

## PL/O编译程序的实现
* 终结符：最小的语法单位，例如构成文法的单词
* 非终结符是一个语法单位，可以由其他一些语法单位组成

BFN范式：  
* `<>`   非终结符，表示待描述的语法成分
* ::=  定义为
* |    或，左部可由多个右部定义  

EBNF范式：
* {}  表示大括号内语法成分可以重复
* `[]` 表示中括号内成分为任意项
* ()  表示小括号内成分优先

### PL/O编译程序的结构
* 一趟扫描方式，以语法语义分析程序为核心
* 当语法分析需要读取单词时就调用词法分析程序，分析正确就用代码生成程序生成目标代码
* 用表格管理程序建立变量、常量和过程标识符的说明与引用之间的信息联系
* 用出错处理程序对词法和语法语义分析遇到的错误给出源程序中出错的位置和错误性质

## 文法和语言
定义：文法G定义为四元组（Vn， Vt， P， S）
* Vn：非终结符集
* Vt：终结符集
* P：规则（a -> b）
  * a属于字母表的闭包（至少包含一个非终结符）
  * b属于字母表闭包
* S：开始符（是一个非终结符）

### 文法的类型
0型、1型、2型、3型（逐渐增加限制）

### 0型文法
也称短语文法、无限制文法  

0型重要理论结果
* 0型文法的能力相当于图灵机
* 任何0型语言都是递归可枚举的
* 递归可枚举的必定是一个0型语言

### 1型文法
也称上下文有关文法  
每个产生式满足：|b|>=|a| （仅S->e除外)

### 2型文法
也称上下文无关文法  
每个产生式满足：a是一个非终结符，b属于字符表闭包

### 3型文法
也称正规文法  
每个产生式为：A->aB 或 A -> a (A,B都为非终结符)
 
 ### 最左/最右推导
 在推导的任何一步推导都是对最左/最右非终结符进行替换  
 * 最右推导被称为规范推导，得到的句型称为规范句型

### 二义
* 文法的二义性（某个句子对应两颗不同的语法树）
* 语言的二义性（上下文无关语言的每一个文法都是二义的）

### 句型的分析
自上而下分析法：从文法的开始符号出发、反复使用各种产生式，寻找匹配于输入串的推导  

自下而上分析法：从输入符号串开始，逐步进行规约，知道归约到文法的开始符

### 句柄
定义：文法G，S是文法的开始符，abc为文法的一个句型
* 短语
* 直接短语（简单短语）
* 一个句型的最左直接短语称为该句型的句柄

### 有关文法的实用限制
* 有害规则：U -> U
* 多余规则：推导用不到的规则
* 某些非终结符不在任何规则的右部出现（不可到达）
* 不能够从这些非终结符推出终结符号串（不可终止）

## 词法分析
* 任务：对源程序进行扫描，产生一个个单词符号
* 单词富豪的种类：
  * 基本字
  * 标识符
  * 常数
  * 运算符
  * 界符  