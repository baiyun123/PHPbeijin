<?php
$arr=array(44,23,66,12,65,7,3,246);
//44,23,3,12,65,7,66,246
//44,23,3,12,7,65,66,246

//���ڱ���������������⣬����$arr��Ҫ��ֵ����&
//$right=count($arr);�˴����ܸ�[$left  $right) ������
function partition(&$arr,$left,$right){
    if ($left==$right-1) {
    	return $left;
    }
        //ȷ���Ƚ�ֵ��λ��
    	$pos=$left;
    	//ȷ���Ƚ�ֵ
    	$key=$arr[$pos];
    	//������������ֵ���Ҽ�ֵ
    	$pl=$left;
    	$pr=$right-1;
	//���������ң����������ң����϶���������Ȼ���˳�ѭ������ʱ�ұߵĿ϶���$key����ߵĿ϶����$keyС��
	while ($pl<$pr){
    	//�ؼ�һ�������������ҵ���һ���ȱȽ�ֵ���ֵ��λ�ú��˳�ѭ����
    	//��$arr[$pl]<$key˵����ߵ�ֵ�ȱȽ�ֵС����������������ѭ�������ҵ��ȱȽ�ֵ���ֵ��Ͳ������������ʿ����˳�ѭ����
    	while ( $pl<$right && $arr[$pl] <= $key ){ $pl++; }
    	//Ȼ���ڴ��ұ��ҵ���һ���ȱȽ�ֵС��ֵ��λ�ú��˳�ѭ��
    	//��$arr[$pr]>$key˵�����ұߵ�ֵ�ȱȽ�ֵ�󣬷�������������ѭ�������ҵ��ȱȽ�ֵС��ֵ��Ͳ����������������˳�ѭ����
    	while ( $pr>=$left && $arr[$pr] > $key){ $pr--; }
    	//��ʱ�ҵ���ߵ�һ����$key���ֵ��λ��$pl���ұߵ�һ����$keyС��ֵ��λ��$pr;
    	//��$pl��$pr��λ�ý��н���;
    	//��ʱ��Ȼ��Ҫ��$pl<$pr�����жϣ���Ϊ��while ($pl<$pr)�˳��������϶���$pr<=$pl,��ʱ���û���жϣ����ֻύ���ȥ��
    	if ($pl<$pr) {
    	$a=$arr[$pl];
    	$arr[$pl]=$arr[$pr];
    	$arr[$pr]=$a;
    	}
	                }
	//����$key��λ�ôӿ�ʼ��һֱû�н�����������ֻ�Ǳ�$key��ĺͱ�$key С��ֵ����������˳�ѭ���Ժ󣬻�Ҫ��$key������ȥ
	//������ʱ���õ�$pr����Ϊ�˳�ѭ���������϶���$pr<=$pl��
	$a=$arr[$pos];
	$arr[$pos]=$arr[$pr];
	$arr[$pr]=$a;
	return $pr;	
}
/* echo partition($arr,0,7);
var_dump($arr); */
//����������⣬��$arr������д�ֵ����&
    function qsort(&$arr,$left,$right){
    	if ($left>=$right){
    		return;
    	}
    	$pos=partition($arr, $left, $right);
    	qsort($arr, $left, $pos);
    	qsort($arr, $pos+1, $right);
        return $arr;	
    }
var_dump(qsort($arr,0,7));

//===============================================
function check_qsort(){
	$arr = array() ;
	for ($j=1;$j<8;$j++){
		$arr[]=rand(2,500);
	}

	$arr1 = array() ;
	foreach($arr as $v) {  $arr1[] = $v; }
	qsort($arr,0,count($arr)) ;
	//����Ǻ��������������
	sort($arr1);

	// ������Ҫ�Ƚ� �������� ��׼������һ����
	$len = count($arr) ; //���鳤��
	$fail = 0 ;
	for($i =0  ; $i<$len ;$i++){
		if ($arr[$i] != $arr1[$i] ) {
			// ����ȣ�˵���������� ..
			$fail  =1;
			break;
		}
	}
	return $fail;
}
function main(){ //������ �����������

	for($c = 0 ; $c < 1000 ;$c++){
		$ret = check_qsort() ; // ret - return ����ֵ����д return�Ƿ��ص���˼
		if ($ret == 1) { // $ret =1 ʧ��
			echo "FAIL" ;
			return;
		}
	}
	echo "OK" ;
}
main();

