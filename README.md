# 專案名稱

余安花店官網

# 簡介

官網中有用到的 BootStrap 排版及 gsap 動畫

### 語言 : 

JavaScript

### 主旨 :

# 快速開始

## 環境建立

- VS Code

## 專案建立

- jQuery、bootstrap、gsap CDN
- 在 <head> 加入

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">

<script src="https://code.jquery.com/jquery-3.5.1.js" integrity="sha256-QWo7LDvxbWT2tbbQ97B53yJnYU3WhH/C8ycbRAkjPDc=" crossorigin="anonymous"></script>
```

- 在 <body> 最下面

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.5.1/gsap.min.js"></script>
```

# 使用範例   

#### Icon動畫-滑鼠進入

```javascript
$(".unIcon").mouseenter(() => {                    
                    gsap.to(".unIcon",{
                        rotate:10
                    }) 
                    unIcon();
                });

function unIcon() {
                gsap.to(".icon-href-1", {
                    duration: 0.5,
                    x: 238,
                    y: 30,
                    opacity: 1,
                });
                gsap.to(".icon-href-2", {
                    duration: 0.5,
                    x: 248,
                    y: 90,
                    opacity: 1,
                });
                gsap.to(".icon-href-3", {
                    duration: 0.5,
                    x: 250,
                    y: 155,
                    opacity: 1,
                });
            }
```

#### Icon動畫-滑鼠離開

```javascript
$(".unIcon").mouseleave(() => {
                    gsap.to(".unIcon",{
                        rotate:0
                    }) 
                    unIconLeave();
                });

function unIconLeave() {
                gsap.to(".icon-href-1", {
                    duration: 0.5,
                    x: 0,
                    y: 0,
                    opacity: 0,
                });
                gsap.to(".icon-href-2", {
                    duration: 0.5,
                    x: 0,
                    opacity: 0,
                });
                gsap.to(".icon-href-3", {
                    duration: 0.5,
                    x: 0,
                    y: 0,
                    opacity: 0,
                });
            }
```

#### Icon連結區塊跳頁

1. 註冊 ScrollToPlugin 並使用

```javascript
gsap.registerPlugin(ScrollToPlugin);
gsap.to(window,{duration:1,scrollTo:{y:".flowers-title"}});
```

#### 照片輪播

1. 加入 slick CDN 

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.9.0/slick.css" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.9.0/slick-theme.css" />
<script src="https://code.jquery.com/jquery-3.5.1.js" integrity="sha256-QWo7LDvxbWT2tbbQ97B53yJnYU3WhH/C8ycbRAkjPDc=" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.9.0/slick.min.js"></script>
```

2. 在 script 中加入

```javascript
$(window).on("load", ()=>{   
	$("selector").slick({
                    autoplay: true,			//自動播放							
                    autoplaySpeed: 0,		//播放完一張要播下一張中的間隔時間
                    draggable: false,		//true為可以拖曳照片false則不行
                    edgeFriction: 0,		
                    centerMode: false,		
                    cssEase: "cubic-bezier(0.950, 0.050, 0.795, 0.035)",	//輪播時的移動效果
                    speed: 5000,			//每一張輪播時間
                    variableWidth: true,	//可以控制輪播圖片的寬度
                    arrows: false,			//輪播左右控制器(箭頭形)true就是顯示;false隱藏
                    pauseOnHover: false,	//鼠標移到輪播圖片上時，true會暫停false則不會
                });
};
```

#### 客製花束的 modal

1. 加入 modal 頁面

```html
<div class="modal fade " role="dialog" style="z-index:3000" tabindex="-1" id="flowers">
            <div class="modal-dialog modal-xl" role="document">
                <div class="modal-content">
                    ......
                </div>         
            </div>
</div>
```

2. 加入 toggle

```html
<div class="col" style="margin-top: -10%" href="#flowers" data-toggle="modal">
    <p>
        按我打開modal
    </p>
</div>
```

#### 客製花束的 modal 內的動畫

1.註冊 ScrollTrigger

```html
gsap.registerPlugin(ScrollTrigger);
```

2.在 script 中加入

```javascript
gsap.from(".flowers-modal", {
                    duration: 1,
                    ease: "none",                    
                    scrollTrigger: {
                        scroller:"#flowers",
                        trigger:".testbbb",
                        start: "10% bottom",
                        end:"85% bottom", 
                        toggleActions:"restart none reverse none"
                    },
                    stagger: {
                        // amount 與 ease 只能存在一個，amount的值是指所有元素的動畫撥放完成的秒數，each則是每個元素動畫播完後下一個元素開始播放之間的間隔秒數
                        // amount: 15,
                        each: 0.1,
                        //from 是指從哪一個元素開始
                        from: 0,
                        //axis要跟grid一起使用，可以讓stagger依照 x軸或是y軸來表演動畫
                        // axis: "y",
                        //grid可以讓動畫指定的全部元素變成二維陣列
                        grid: [0,1],
                        //stagger 內的onComplete 是指一個元素撥放完動畫後就執行一次，此demo會執行25次
                        onComplete: () => {
                        },
                    },
                    //當25個元素的動畫都撥放完畢會執行的onComplete
                    onComplete: () => {
                    },
                    opacity: 0,
                });
```





# 觀念

- slick JS CDN 一定要在 jquery JS CDN後面

