title: php实现图片自动水印
tags:
  - php
  - 图片
  - 水印
  - 自动
id: 92
categories:
  - Code
date: 2012-02-07 09:22:23
---

一个php的function，从一个类里面扒拉出来的，默认把水印打在图片右下角，边距10。从$list数组中取得图片地址，$list中$list[0]为图片张数，后续依次为图片地址。水印为同目录下watermark.png，水印完成后自动把图片复制到$dir目录下，成功返回值为1，否则为0.
<pre class="lang:default decode:true ">&lt;?php
function watermark($list,$dir){
	$check = 1;
	$n = $list[0];
	$waterImage = "watermark.png";

	$water_info = getimagesize($waterImage);
	$water_w = $water_info[0];
	$water_h = $water_info[1];

	$water_im = imagecreatefrompng($waterImage);

	for($i=1;$i&lt;=$n;$i++){
		$groundImage = $list[$i];

		$m = $i;
		if($m&lt;10){$m="0".$m.".jpg";}else{$m=$m.".jpg";}

		$ground_info = getimagesize($groundImage);

		$ground_w = $ground_info[0];
		$ground_h = $ground_info[1];

		$ground_im = imagecreatefromjpeg($groundImage);

		$posX = $ground_w - $water_w - 10;
		$posY = $ground_h - $water_h - 10;

		imagealphablending($ground_im, true);
		imagecopy($ground_im, $water_im, $posX, $posY, 0, 0, $water_w,$water_h);

		imagejpeg($ground_im,$m,100);

		if(!copy($m,$dir."/".$m)){$check=0;}
		@unlink($m);

	}

	if(isset($water_info)) unset($water_info);
	if(isset($water_im)) imagedestroy($water_im);
	unset($ground_info);
	imagedestroy($ground_im);

	return $check;

}
?&gt;</pre>
&nbsp;