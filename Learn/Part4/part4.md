# 第四章重点： #

***

## 变量的声明方式  ##

	var s string
	var s2 = string("shijie")
	s1 := "wenxuwan"
	fmt.Println(s,s1,s2)
	
	第一种方式是最传统的变量声明方式，可以显式的看到变量的类型。
	第二种是利用go语言的类型推断，在声明s2的时候我们不需要定义s2的类型，它会根据后面表达式返回类型来自动判断s2类型
	第三种是在go语言的推断上加了点语法糖，只能在函数内部使用，或者写for，if,switch语句的时候用在初始化语句中来声明一些临时的变量。不能作为全局声明。

##go语言的类型推断有哪些好处##

	1. 可以不用自己敲那么多声明
	2. 代码重构的时候（代码重构指的是“不改变某个程序与外界的交互方式和归结，只改变函数内部实现。也就是暴露出来的接口的参数，名字，返回值不变”）方便，不需要关注函数内部返回值的变化。
	3. 因为go语言的是静态语言，变量类型在编译期间就确定了，所以不会影响到函数的执行效率。

***	
## 函数重声明的意思 ##
	
	函数重声明主要是用短变量声明对同一个代码块下面的变量进行声明

**代码块概念：**

	个人认为只要大括号扩起来就算一个模块
***

## 重声明的前提条件##

	1.再次声明的时候要和前面声明的类型一致
	2.声明和重声明要在同一代码块下，不然就相当于局部变量覆盖全局变量
	3.重声明只有在短变量声明的时候才会发生，不然用var声明两个同名的变量会提示冲突
	4.重声明的时候一定要保证至少有一个变量是新的。
		func main() {
			var s string
			var s2 = string("old")
			s2 := string("new") //error,no new variables on left side of :=
			fmt.Println(s,s2)
		}
		
## 思考题目 ##

如果与当前变量重名的是外层代码中的变量，这意味着什么？

	var s2 = string("out")
	func main() {
		var s string
		{
			s2 := string("internal")
			fmt.Println(s,s2)
		}
		fmt.Println(s2)
	}

	output: internal  out
	局部变量会隐藏外部变量