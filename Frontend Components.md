Manually Sliding
===================
#### HTML
```html
		<div class="container">
			<div style="float: left; width: 100%; height: 90%"	class="mySlides"></div>
			<div style="float: left; width: 100%; height: 90%" class="mySlides"></div>
			<a class="w3-btn-floating"	style="position: absolute; top: 45%; left: 0" onclick="plusDivs(-1)">❮</a>
			<a class="w3-btn-floating"	style="position: absolute; top: 45%; right: 0" onclick="plusDivs(1)">❯</a>
			<div style="position: absolute; bottom: 0; left: 50%">
				<div class="navigator" style="position: relative; left: -50%; width: 600px">
					<ul>
						<li><a href="#" class="active">Item 1</a></li>
						<li><a href="#">Item 2</a></li>
						<li><a href="#">Item 3</a></li>
						<li><a href="#">Item 4</a></li>
					</ul>
					<span></span>
				</div>
			</div>
		</div>
````
#### CSS
````css
.w3-btn-floating:hover{box-shadow:0 8px 16px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19)}
.w3-btn-floating{-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}   
.w3-btn-floating{display:inline-block;text-align:center;color:#fff;background-color:#000;position:relative;overflow:hidden;z-index:1;padding:0;border-radius:50%;cursor:pointer;font-size:24px;}
.w3-btn-floating{width:40px;height:40px;line-height:40px}

div.navigator ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

div.navigator li {
    float: left;
}

div.navigator a:link, div.navigator a:visited {
    font-weight: bold;
    color: #FFFFFF;
    background-color: #bebebe;
    text-align: center;
    padding: 7px 0;
    text-decoration: none;
}

div.navigator a {
    display: block;
    margin-left: 20px;
    width: 120px;
}

div.navigator a:hover,div.navigator a:active {
	background-color:#4f81bd;
}
.active {
	background-color:#4f81bd !important;
}
````
#### JavaScript
````javascript
<script>
var slideIndex = 1; //default slide
showDivs(slideIndex);

function plusDivs(n) {
  showDivs(slideIndex += n);
}

function showDivs(n) {
  var i;
  var x = document.getElementsByClassName("mySlides");
  if (n > x.length) {slideIndex = 1}
  if (n < 1) {slideIndex = x.length}
  for (i = 0; i < x.length; i++) {
     x[i].style.display = "none";
  }
  x[slideIndex-1].style.display = "block";
}

$(function(){
	$("[href='#']").click(function(){
		$(".active").removeClass("active");
		 $(this).addClass("active");
		 var order = $(this).attr('order');
		 //showDivs(order); TODO need to be implemented
	  })
})
</script>
````
