teacher_add_school
<?php
header("content-type:text/html;charset=gbk");
//���������࣬�������ʦ������뵽ѧУ�����У�ֻ�ܽ���ʦ����ʵ������Ȼ����ӵ�ѧУ�ĳ�Ա�����������У�Ȼ��ѭ��������飬�õ���ʦ�࣬
//Ȼ���������ĳ�Ա���Դ�ʱ����������ϰ��һ��
class school{
	public $name;
	//�������飬��ӵ������е���ʵ���������ʦ��
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
//����һ��������ѧУ����ӵ���ʦ�������
function show(){
//ʵ����ѧУ���˴���Ҫ��ûʵ����һ���࣬��������ǰ��ʵ�����������ȫ����ͬ�ģ�
//��ͺ�����ࡣ���������������
$school=new school();
$school->set_name("����һ��");
//ʵ������ʦ�࣬���һ����ʦ
$teacher=new teacher();
$teacher->set_name("��");
$teacher->set_age("19");
//����Ĳ����Ƕ���ʦ���ڵĳ�Ա���Խ��и�ֵ
//�����ǽ���ֵ�õ�����ӵ�ѧУ���ڵĳ�Ա���� ������ȥ
$school->add_teacher($teacher);

//ʵ����һ���µ���ʦ�࣬�����һ����ʦ
$teacher=new teacher();
$teacher->set_name("��");
$teacher->set_age("18");
//����Ĳ����Ƕ���ʵ������ʦ���ڵĳ�Ա���Խ��и�ֵ
//�����ǽ���ֵ�õ�����ӵ�ѧУ���ڵĳ�Ա���� ������ȥ
$school->add_teacher($teacher);

//ͬ�ϣ�ע��Ϊʲôÿ�ζ�Ҫʵ����һ����
$teacher=new teacher();
$teacher->set_name("��");
$teacher->set_age("20");
//����Ĳ����Ƕ���ʵ������ʦ���ڵĳ�Ա���Խ��и�ֵ��ע��ÿ����ʵ��������ʦ���ǰ��ʵ���������ʦ������ȫ��ͬ��
//�����ǽ���ֵ�õ�����ӵ�ѧУ���ڵĳ�Ա���� ������ȥ
$school->add_teacher($teacher);
 
//���Ĺؼ�һ����     �����ӵ�$school->add_teacher�����е���ʵ�������ÿһ����ʦ��

echo $school->get_name();
foreach ($school->teacher_name as $var){
 //��$school->add_teacher������б��������ÿһ��$var��һ��ʵ��������ʦ��
 //ÿ�ζ���ʦ���ڵĳ�Ա���� name  �� age���з������
	echo $var->name;
	echo $var->age;
}
}

show();
