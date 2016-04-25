<?php
$arr=array(44,23,66,12,65,7,3,246);
//44,23,3,12,65,7,66,246
//44,23,3,12,7,65,66,246

//由于变量的作用域的问题，这里$arr需要传值，用&
//$right=count($arr);此处不能改[$left  $right) 开区间
function partition(&$arr,$left,$right){
    if ($left==$right-1) {
    	return $left;
    }
        //确定比较值的位置
    	$pos=$left;
    	//确定比较值
    	$key=$arr[$pos];
    	//定义数组的左键值和右键值
    	$pl=$left;
    	$pr=$right-1;
	//从左向右找，从右向左找，最后肯定会相遇，然后退出循环，此时右边的肯定比$key大，左边的肯定会比$key小，
	while ($pl<$pr){
    	//关键一步，从左向右找到第一个比比较值大的值的位置后，退出循环；
    	//当$arr[$pl]<$key说明左边的值比比较值小，符合条件，进入循环；当找到比比较值大的值后就不符合条件，故可以退出循环；
    	while ( $pl<$right && $arr[$pl] <= $key ){ $pl++; }
    	//然后在从右边找到第一个比比较值小的值的位置后，退出循环
    	//当$arr[$pr]>$key说明，右边的值比比较值大，符合条件，继续循环，当找到比比较值小的值后就不符号条件，可以退出循环；
    	while ( $pr>=$left && $arr[$pr] > $key){ $pr--; }
    	//此时找到左边第一个比$key大的值的位置$pl和右边第一个比$key小的值的位置$pr;
    	//把$pl和$pr的位置进行交换;
    	//此时任然需要对$pl<$pr进行判断，因为在while ($pl<$pr)退出的条件肯定是$pr<=$pl,此时如果没有判断，就又会交替回去；
    	if ($pl<$pr) {
    	$a=$arr[$pl];
    	$arr[$pl]=$arr[$pr];
    	$arr[$pr]=$a;
    	}
	                }
	//由于$key的位置从开始都一直没有交换，交换的只是比$key大的和比$key 小的值，所以最后退出循环以后，还要把$key交换回去
	//交换的时候用的$pr是因为退出循环的条件肯定是$pr<=$pl；
	$a=$arr[$pos];
	$arr[$pos]=$arr[$pr];
	$arr[$pr]=$a;
	return $pr;	
}
/* echo partition($arr,0,7);
var_dump($arr); */
//作用域的问题，对$arr必须进行传值，用&
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
	//这个是函数库里面的排序
	sort($arr1);

	// 接下来要比较 你的排序跟 标准排序是一样的
	$len = count($arr) ; //数组长度
	$fail = 0 ;
	for($i =0  ; $i<$len ;$i++){
		if ($arr[$i] != $arr1[$i] ) {
			// 不相等，说明有问题了 ..
			$fail  =1;
			break;
		}
	}
	return $fail;
}
function main(){ //主函数 ，从这里进入

	for($c = 0 ; $c < 1000 ;$c++){
		$ret = check_qsort() ; // ret - return 返回值的缩写 return是返回的意思
		if ($ret == 1) { // $ret =1 失败
			echo "FAIL" ;
			return;
		}
	}
	echo "OK" ;
}
main();

