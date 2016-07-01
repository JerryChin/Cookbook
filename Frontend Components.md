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
/**
 * 
 */
function EasySlide(containerId, defaultItemPos) {
	this.containerId = containerId;
	this.wrappers = document.querySelectorAll(containerId + " .wrapper");
	this.links = document.querySelectorAll(containerId + " .itemLinks");
	this.activeItemPos = -1;
	this.defaultItemPos = defaultItemPos;
	return this;
}

EasySlide.prototype.previousItem = function() {
	if(this.activeItemPos == 0)
		this.activeItemPos = this.links.length;
	this.changePosition(this.links[--this.activeItemPos]);
}

EasySlide.prototype.nextItem = function() {
	if(this.activeItemPos == this.links.length - 1)
		this.activeItemPos = -1;
	this.changePosition(this.links[++this.activeItemPos]);
}

EasySlide.prototype.changePosition=function(link) {
    this.removeActiveLinks();
 	this.hideActiveWrapper();
	var position = link.getAttribute("data-pos");
	this.activeItemPos = position;
	$(this.wrappers[position]).css("display","block");
	$(link).addClass("active");
}

EasySlide.prototype.addItemListener = function() {
	var retention = this;
	// setup the event listeners
	for (var i = 0; i < this.links.length; i++) {
	    $(this.links[i]).click(function(e) {
	    	retention.setClickedItem(e);
	    });
	}
	return this;
}

EasySlide.prototype.setClickedItem = function(e) {
    this.changePosition(e.target);
}

EasySlide.prototype.removeActiveLinks = function() {
	for (var i = 0; i < this.links.length; i++) {
        $(this.links[i]).removeClass("active");
    }
}

EasySlide.prototype.hideActiveWrapper = function() {
	for (var i = 0; i < this.wrappers.length; i++) {
        $(this.wrappers[i]).css("display", "none");
    }
}

EasySlide.prototype.init = function() {
	var retention = this;
	$(function(){
		setTimeout(function() {
			$(retention.containerId + " .upper-btn-left").click(function(){
				retention.previousItem();
			});
			$(retention.containerId + " .upper-btn-right").click(function(){
				retention.nextItem();
			});
			retention.addItemListener().changePosition(retention.links[retention.defaultItemPos]);
	}, 10);
	});
}
````
