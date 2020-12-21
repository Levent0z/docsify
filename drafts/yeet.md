# Yeet

```JavaScript
document.querySelector('[jsname=RFn3Rd']).childElementCount
```

Add Toggle side button under this:
class="lvE3se"

To add the button:
```JavaScript
var parent = document.querySelector('.NzPR9b')
var newdiv = document.createElement('div');
newdiv.classList.add(...['uArJ5e', 'UQuaGc', 'kCyAyd', 'kW31ib', 'foXzLb']);
newdiv.style.display = 'flex';
newDiv.innerHTML = // SVG viewBox = 0 0 24 24 ( width: 24px height: 24px)
parent.insertAdjacentElement('afterbegin', newdiv)
```


Main: class="xsj2Ff Zf0RDc AwnI1b"
Take its width (W), translate it (window.clientWidth - W)

Side items:
class="xsj2Ff Zf0RDc PoIECb GskdZ AwnI1b vLRPrf" 
class="xsj2Ff Zf0RDc PoIECb vLRPrf AwnI1b"






---------


xsj2Ff Zf0RDc PoIECb GskdZ vLRPrf AwnI1b


MAIN : class="xsj2Ff Zf0RDc GskdZ AwnI1b"


When Vertical:
large video --> class="xsj2Ff Zf0RDc GskdZ AwnI1b"
small video --> class="xsj2Ff Zf0RDc PoIECb AwnI1b"

let second = pv.querySelector(`.${childViewId}[data-allocation-index="1"]`);
undefined
second.style.top
"0px"
first.style.width
"2133px"
first.parentElement.clientWidth
2844


first.parentElement.clientWidth - parseInt(first.style.width)
711
first.style.transform = "translateX(711px)"

others.forEach(node => { node.style.transform = `translateX(-${first.style.width})`; })

------

Tiled (presenting)
pv.classList

DOMTokenList(8) ["zWfAib", "Z319Jd", "__gmgv-btb-resize", "__gmgv-rtb-resize", "Qtgubc", "t4HJue", "a1pVef", "CUJC3", value: "zWfAib Z319Jd __gmgv-btb-resize __gmgv-rtb-resize Qtgubc t4HJue a1pVef CUJC3"]


----

Pinned child item:
date-allocation-index = 0
xsj2Ff Zf0RDc PoIECb AwnI1b vLRPrf


Add Z-index to data-allocation-index


Other presenting in auto mode:
zWfAib Z319Jd __gmgv-btb-resize __gmgv-rtb-resize Qtgubc a1pVef CUJC3



--------
Not presenting:
document.querySelector('.zWfAib').classList
DOMTokenList(6) ["zWfAib", "Z319Jd", "t4HJue", "eFmLfc", "a1pVef", "CUJC3", value: "zWfAib Z319Jd t4HJue `eFmLfc` a1pVef CUJC3"]

Presenting:
document.querySelector('.zWfAib').classList
DOMTokenList(6) ["zWfAib", "Z319Jd", "t4HJue", "a1pVef", "CUJC3", "Qtgubc", value: "zWfAib Z319Jd t4HJue a1pVef CUJC3 `Qtgubc`"]

Item Pinned (not presenting):
document.querySelector('.zWfAib').classList
DOMTokenList(5) ["zWfAib", "Z319Jd", "n9oEIb", "QhPhw", "a1pVef", value: "zWfAib Z319Jd `n9oEIb` QhPhw a1pVef"]

Item Pinned (presenting, of presentation):
document.querySelector('.zWfAib').classList
DOMTokenList(5) ["zWfAib", "Z319Jd", "n9oEIb", "QhPhw", "a1pVef", value: "zWfAib Z319Jd `n9oEIb` QhPhw a1pVef"]

Item Pinned (presenting, of presenter):
document.querySelector('.zWfAib').classList
DOMTokenList(6) ["zWfAib", "Z319Jd", "n9oEIb", "QhPhw", "a1pVef", "CUJC3", value: "zWfAib Z319Jd n9oEIb QhPhw a1pVef CUJC3"]


document.querySelector('.zWfAib > [data-allocation-index="0"]').style.width
"536px"
document.querySelector('.zWfAib > [data-allocation-index="0"]').clientWidth
536


document.querySelector('.zWfAib > [data-allocation-index="0"]').style.left = "calc(100vw - 536px)"
Use this instead to accomodate opening of the sidebar
document.querySelector('.zWfAib > [data-allocation-index="0"]').style.left = "calc(100% - 536px)"




document.querySelectorAll('.zWfAib > :not([data-allocation-index="0"])')[0].style.transform = 'translate(20px, 20px)'


When somebody leaves, styles are reset
When something is pinned, it's the only child of .zWfAib with data-allocation-index="0"

When the sidebar appears:
.mKBhCf.kjZr4 {
    transition-delay: .24s;
    transition-timing-function: cubic-bezier(0.0,0.0,0.2,1);
    transform: translate3d(0,0,0);
}
.mKBhCf.qwU8Me {
    transform: translate3d(100%,0,0);   /* overridden above */
    right: 0;
}



When landscape and presenting:
document.querySelector('.zWfAib > [data-allocation-index="0"]').clientHeight
716
document.querySelector('.zWfAib').clientHeight
713
document.querySelector('.zWfAib').clientWidth
2844
document.querySelector('.zWfAib > [data-allocation-index="0"]').clientWidth
1432

When portrait and presenting
document.querySelector('.zWfAib').clientWidth
1679
document.querySelector('.zWfAib > [data-allocation-index="0"]').clientWidth
1679
document.querySelector('.zWfAib').clientHeight
1193
document.querySelector('.zWfAib > [data-allocation-index="0"]').clientHeight
873