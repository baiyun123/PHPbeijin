teacher_add_school
<?php
header("content-type:text/html;charset=gbk");
//设置两个类，如果把老师的类加入到学校的类中，只能将老师的类实例化，然后添加到学校的成员方法的数组中，然后循环输出数组，得到老师类，
//然后访问类里的成员属性此时将两个类练习到一起
class school{
	public $name;
	//设置数组，添加到数组中的是实例化后的老师类
	public $teacher_name=array();
	function set_name($name){
		$this->name=$name;
	}
	function get_name(){
		return $this->name;
	}
	function add_teacher($teacher_name){
		$this->teacher_name[]=$teacher_name;
	}
}
class teacher{
	public $name;
	public $age;
	function set_name($name){
		$this->name=$name;
	}
	function set_age($age){
		$this->age=$age;
	}
}
//设置一个函数将学校里添加的老师都输出来
function show(){
//实例化学校，此处主要，没实例化一个类，这个类和以前的实例化后的类完全不相同的，
//类和函数差不多。都有作用域的问题
$school=new school();
$school->set_name("柳林一中");
//实例化老师类，添加一名老师
$teacher=new teacher();
$teacher->set_name("张");
$teacher->set_age("19");
//上面的部分是对老师类内的成员属性进行赋值
//下面是将赋值好的类添加到学校类内的成员属性 数组中去
$school->add_teacher($teacher);

//实例化一个新的老师类，在添加一名老师
$teacher=new teacher();
$teacher->set_name("李");
$teacher->set_age("18");
//上面的部分是对新实例化老师类内的成员属性进行赋值
//下面是将赋值好的类添加到学校类内的成员属性 数组中去
$school->add_teacher($teacher);

//同上，注意为什么每次都要实例化一个类
$teacher=new teacher();
$teacher->set_name("刘");
$teacher->set_age("20");
//上面的部分是对新实例化老师类内的成员属性进行赋值，注意每次新实例化的老师类和前面实例化后的老师类是完全不同的
//下面是将赋值好的类添加到学校类内的成员属性 数组中去
$school->add_teacher($teacher);
 
//理解的关键一步是     最后添加到$school->add_teacher数组中的是实例化后的每一个老师类

echo $school->get_name();
foreach ($school->teacher_name as $var){
 //对$school->add_teacher数组进行遍历输出，每一个$var是一个实例化的老师类
 //每次对老师类内的成员属性 name  和 age进行访问输出
	echo $var->name;
	echo $var->age;
}
}

show();
