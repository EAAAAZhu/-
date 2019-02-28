# -<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title></title>
<style type="text/css">
#box{position: absolute;top: 150px;left: 250px;width: 200px;height: 200px;background-color: red;}
</style>
<script type="text/javascript">
window.onload=function(){
	var oBox=document.getElementById('box');
	var b='';//声明两个空变量a，b；
	var a='';
	oBox.onmousedown=function(ev){
		var iEvent=ev||event;
		var dx=iEvent.clientX;//当你第一次单击的时候，存储x轴的坐标。
		var dy=iEvent.clientY;//当你第一次单击的时候，储存Y轴的坐标。
		var dw=oBox.offsetWidth;//存储默认的div的宽度。
		var dh=oBox.offsetHeight;//存储默认的div的高度。
		var disright=oBox.offsetLeft+oBox.offsetWidth;//存储默认div右边距离屏幕左边的距离。
		var distop=oBox.offsetHeight+oBox.offsetTop;//存储默认div上边距离屏幕左边的距离。
		if(iEvent.clientX>oBox.offsetLeft+oBox.offsetWidth-10){//判断鼠标是否点在右边还是左边，看图1理解
			b='right';
		}
		if(iEvent.clientX<oBox.offsetLeft+10){//同理
			b='left';
		}
		if(iEvent.clientY<oBox.offsetTop+10){
			a='top';
		}
		if(iEvent.clientY>oBox.offsetTop+oBox.offsetHeight-10){
			a='bottom';
		}
		document.onmousemove=function(ev){
			var iEvent=ev||event;
			if(b=='right'){
				oBox.style.width=dw+(iEvent.clientX-dx)+'px';
				//此时的iEvent.clientX的为你拖动时一直改变的鼠标的X坐标，例如你拖动的距离为下图的绿色部分，第二个黑点就表示你此时的iEvent.clientX
				//所以，此时的盒子宽度就等于绿色部分的距离加上原本盒子的距离，看图2
				if(oBox.offsetWidth<=10){//当盒子缩小到一定范围内的时候，让他保持一个固定值，不再继续改变
					oBox.style.width='10px';
				}
			}
			if(b=='left'){
				oBox.style.width=dw-(iEvent.clientX-dx)+'px';//iEvent.clientX-dx表示第二次鼠标的X坐标减去第一次鼠标的X坐标，得到绿色移动的距离（为负数），再加上原本的div宽度，就得到新的宽度。 图3
				oBox.style.left=disright-oBox.offsetWidth+'px';//disright表示盒子右边框距离左边的距离，disright-当前的盒子宽度，就是当前盒子距离左边的距离
				if(oBox.offsetWidth<=10){
					oBox.style.width='10px';
					oBox.style.left=disright-oBox.offsetWidth+'px';//防止抖动
				}
			}	
			if(a=='bottom'){
				oBox.style.height=iEvent.clientY-dy+dh+'px';
				if(oBox.offsetHeight<=10){
					oBox.style.height='10px';
				}
			}
			if(a=='top'){
				oBox.style.height=dh-(iEvent.clientY-dy)+'px'
				oBox.style.top=distop-oBox.offsetHeight+'px';
				if(oBox.offsetHeight<=10){
					oBox.style.height='10px';
					oBox.style.top=distop-oBox.offsetHeight+'px';
				}
			}
		};
		document.onmouseup=function(){
		document.onmousedown=null;
		document.onmousemove=null;
		};
		return false;
	};
};
</script>
</head>
<body>
<div id="box"></div>
</body>
</html>
</p>
