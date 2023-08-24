title: easypiechart通过AJAX获取Json数据，动态刷新
author: Mia Liu
tags:
  - easypiechart
categories:
  - 前端
date: 2018-04-20 17:47:00
---
**这是我寄几写来记录的，有需要的可以参考，如果有不对的地方欢迎指正 QAQ**
首先需要引用JQ和easypiechart相关js
我们的需求是，一进入页面为了保证加载快一点，先给定一个值，然后每三秒钟根据后台传来的json文件刷新数据，话不多说，上图。这是初始情况下的echart。
![start](http://upload-images.jianshu.io/upload_images/4620451-154d9fc4af816946.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

					<li>
						<div id="pie_1" class="piechart"
							data-percent="0">
							<span class="percent"></span>
						</div> <span class="title">连网状态 </span>
					</li>
					<li>
						<div id="pie_2" class="piechart"
							data-percent="0"> 
							<span class="percent"></span>
						</div> <span class="title">云服务</span>
					</li>
					<li>
						<div id="pie_3" class="piechart"
							data-percent="18"> 
							<span class="percent"></span>
						</div> <span class="title">远程运维</span>
					</li>
					<li>
						<div id="pie_4" class="piechart" data-percent="85">
							<span class="percent"></span>
						</div> <span class="title">版本升级</span>
					</li>
				

以上是初始情况下的HTML。
下面上js。

<pre>
var chart1;
var chart2;
var chart3;
var handleProfileSkillPie = function () {
	//Pie 1
	$('#pie_1').easyPieChart({
		easing: 'easeOutBounce',
		onStep: function(from, to, percent) {
			$(this.el).find('.percent').text(Math.round(percent)+"%");
		},
		lineWidth: 6,
		barColor: '#F0AD4E'
	});
	 chart1 = window.chart = $('#pie_1').data('easyPieChart');
	//Pie 2
	$('#pie_2').easyPieChart({
		easing: 'easeOutBounce',
		onStep: function(from, to, percent) {
			$(this.el).find('.percent').text(Math.round(percent)+"%");
		},
		lineWidth: 6,
		barColor: '#D9534F'
	});
	chart2 = window.chart = $('#pie_2').data('easyPieChart'); 
	//Pie 3
	$('#pie_3').easyPieChart({
		easing: 'easeOutBounce',
		onStep: function(from, to, percent) {
			$(this.el).find('.percent').text(Math.round(percent)+"%");
		},
		lineWidth: 6,
		barColor: '#70AFC4'
	});
	chart3 = window.chart = $('#pie_3').data('easyPieChart'); 
	}
	 handleProfileSkillPie();
</pre>

接下来是AJAX。

<pre>
	 function loadnumber(){
		 var all;
		 var num;
		 var cloud;
		 var control;
		 $.ajax({
		    url:'数据来源json文件的url',
		    type:'get',
		    dataTpye:'json',
		    cache:false,
		    async:true,
		    success:function(data){
		    		all=data.allCount;
		    		var number=data.statusCount;
		    		num=number.networkStatus;
		    		cloud=number.cloudStatus;
		    		control=number.controlStatus;		    		   		
                    $('#pie_1').attr('data-percent',Math.round(num/all));
		    		$('#pie_2').attr('data-percent',Math.round(cloud/all));
		    		$('#pie_3').attr('data-percent',Math.round(control/all)); 		 	
		    		$('#pie_1 .percent').text(Math.round(num/all)+"%");
		    		$('#pie_2 .percent').text(Math.round(cloud/all)+"%");
		    		$('#pie_3 .percent').text(Math.round(control/all)+"%");
		  		
<p>	
		 `//这里重画easypiechart `
		    		
		    		chart1.update(Math.round(num/all));
		    		chart2.update(Math.round(cloud/all));
		    		chart3.update(Math.round(control/all));
		    		
		    	}	
		 })
		 }

		 $(document).ready(function(){
		 	  window.setInterval(loadnumber,3000);
		 	})
</pre>



![done](http://upload-images.jianshu.io/upload_images/4620451-c2142cde90a5223b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


大功告成咯，真好玩，这是动态的局部刷新，我不会搞动图进来，so,就酱~