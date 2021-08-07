# Stripe-Follow-Along-Nav
实现当鼠标经过小标题时，出现二级菜单，需要注意，二级菜单是大小不一的
效果：https://xl-z4869.github.io/Stripe-Follow-Along-Nav/index.html
### 一、知识点
#### Element.getBoundingClientRect()
https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect
### 二、主要步骤
#### 1.获得主要元素
```
const nav = document.querySelector('.top')
const lis = document.querySelectorAll('.cool>li')
const dropdownBackground = document.querySelector('.dropdownBackground')
```
#### 2.给所有li监听鼠标进入事件
* 当鼠标经过时，显示二级菜单
* 获得对应二级菜单的宽高等属性
* 给白色背景添加宽高等
```
function enterHandler() {
    this.classList.add('trigger-enter')
    setTimeout(() => this.classList.contains('trigger-enter') && this.classList.add('trigger-enter-active'), 150);
    dropdownBackground.classList.add('open');
    const dropdown = this.querySelector('.dropdown')
        // console.log(dropdown);
    const navRect = nav.getBoundingClientRect();
    const dropdownRect = dropdown.getBoundingClientRect()
    const coords = {
        height: dropdownRect.height,
        width: dropdownRect.width,
        top: dropdownRect.top - navRect.top,
        left: dropdownRect.left - navRect.left
    }
    dropdownBackground.style.setProperty('width', `${coords.width}px`)
    dropdownBackground.style.setProperty('height', `${coords.height}px`)
    dropdownBackground.style.setProperty('transform', `translate(${coords.left}px,${coords.top}px)`)
}


lis.forEach(li => li.addEventListener('mouseenter', enterHandler))
```
#### 3.添加鼠标移出事件
将二级菜单以及白色背景内容隐藏
```
function leaveHandler() {
    this.classList.remove('trigger-enter', 'trigger-enter-active')
    dropdownBackground.classList.remove('open')
}

lis.forEach(li => li.addEventListener('mouseleave', leaveHandler))
```
