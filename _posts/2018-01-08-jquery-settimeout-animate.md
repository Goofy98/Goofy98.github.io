---
layout: post
title:  "jQuery的settimeout和animate细节"
categories: jQuery
date:   2018-01-08 13:48:05
author: Goofy
tags:  jQuery
---

* content
{:toc}

# jQuery与setTimeOut
setTimeOut内并不支持$(this)会变成windows的$(this)
```js
var is = $(this);  //所以首先把$(this)赋值
t=setTimeout(function(){               	
  $(is).children("ul").animate({   //这样setTimeOut里面$(this)就可以继承使用了
      'top': 40 + 'px',
      'opacity': 1
  }, 200)
},1000);
}
```

# jQuery与animate

animate 并不支持display，所以想要使用display只能使用JQ中的show（）和hide（）或fadeIn（）和fadeOut（）

## animate 中使用show（）和hide（）

- 显示 ：  `show()`  
- 隐藏： `hide()` 因为hide（）执行是没有时间的所以直接放上去会连动画都没显示就直接隐藏了
- 动画hide ： `hide(1)` 给hide()加个时间就可以完美解决了。
```js
 function(){
                      var is = $(this);
                      t=setTimeout(function(){               	
                          $(is).children("ul").animate({
                              'top': 40 + 'px',
                              'opacity': 1
                          }, 200)
                      $(is).children("ul").show();
                      },1000);
                  },
                  function(){
                      clearTimeout(t);
                      
                      $(this).children("ul").animate({
                          'top': 50 + 'px',
                      'opacity' : 0
                      }, 200)
                   $(this).children("ul").hide(1);                  
                  }
                  );
          });
```

## animate 中使用fadeIn（）和fadeOut（）

- 显示 ： `fadeIn()` 
- 隐藏 ： `fadeOut()` 
- 因为fadeIn（）和fadeOut（）两个都自带动画效果和动画时间当他们和animate同时使用的时候会有顺序关系所以需要把fadeIn（）和fadeOut（）的时间给缩短
- 显示 ： `fadeIn(1)` 
- 隐藏 ： `fadeOut(1)` 

```js
 function(){
                      var is = $(this);
                      t=setTimeout(function(){               	
                          $(is).children("ul").animate({
                              'top': 40 + 'px',
                              'opacity': 1
                          }, 200)
                      $(is).children("ul").fateIn(1);
                      },1000);
                  },
                  function(){
                      clearTimeout(t);
                      
                      $(this).children("ul").animate({
                          'top': 50 + 'px',
                      'opacity' : 0
                      }, 200)
                   $(this).children("ul").fateOut(1);                  
                  }
                  );
          });
```