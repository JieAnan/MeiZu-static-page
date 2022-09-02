

# 1.行内元素如何设置元素高度？
             比如a标签不能直接设置高度，应该转化为行内块元素 dispaly:inline-block
             或者使用position中的 absolute定位或者fixed定位

# 2.如何给一个购物车添加鼠标mouseenter事件，当鼠标移动到上面时候，显示其下拉框？
    
    1.显示下拉框，属于元素重叠，考虑使用定位中的【子绝父相】，其中子元素使用绝对定位能够使元素脱标，不占有位置。

    2.其下拉框的显示与隐藏实现方式脑阔两种：
       其一就是使用 display来控制其显示与隐藏，但是不能添加transition变化动画。

       其二就是使用height从0到100的方式，初始高度为0px，当点击时候设置为100px从而控制盒子的显示与隐藏。
       注意：初始height为0px时候需要搭配overflow控制字体溢出进行隐藏：hidden。
  
# 3.在将span元素li元素等转化为inline-block元素时候，默认使用多个分行排列的li元素会在页面显示很小的空格。
    原因是：当元素换行显示时候元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据white-space的处理方式（默认是normal，合并多余空白），原来HTML代码中的回车换行被转成一个空白符，所以元素之间就出现了空隙。这些元素之间的间距会随着字体的大小而变化，当行内元素font-size:16px时，间距为8px。
     
    解决办法：最简单的方式是：在其li元素的父级元素中设置font-size：0px,来去除该空白值。span元素同理。

# 4.布局技巧：
    pc端布局中，如果不需要响应式布局，想要同一行显示，直接加浮动。
               浮动完成之后调节盒子之间的距离。使用绝对定位。
    移动端布局：多用弹性盒子模型。

    无序列表： ul > li > a

    下拉框：①绝对定位 ② 默认隐藏 ③鼠标悬停出现。
            .children {
                      position: absolute;
                      top: 40px;
                      right: 0px;
                      height: 0px;
                      width: 300px;
                      background-color: #fff;
                      box-shadow: 0 2px 10px rgba(0, 0, 0, .15);
                      color: #424242;
                      transition: all .3s;
                      /*高度设置为0  文字溢出*/
                      overflow: hidden;
                      z-index: 100;
                    }
          .father:hover {
                      background-color: #fff;

                      a {
                        color: #ff6700;
                      }

                      .children {
                        height: 100px;
                        line-height: 100px;
                      }
                    }
    可以使用过渡transtion的属性：
       颜色  数值   阴影 转换

    自绝父相的居中： 1.left：50%
                    2. margin-left:负的宽度一半。
    布局方式：1.可以使用块级元素包裹行内元素
             2.尽量不要使用行内元素a包括块级元素div p等等 
    绘制三角形：三部曲
            1.设置宽高为0px
            2.去除目标三角形的对面边框
            3.设置另外两个边框颜色为transperant

    绘制扇形：三部曲
            1.设置宽高0px
            2.设置所有边框为透明transparent。
            3.设置border-radius的大小
            4.设置目标扇形的颜色。

    元素同一行显示：使用float进行左浮动和右浮动。

  # 5.搜索框布局：
        布局1
            外层div：设置边框
            内层左边：input框输入文本  
            内层右边：button按钮框选择

        布局2
            左边：input框输入文本 + 边框
            右边：button按钮框选择 + 边框

    tips:
    1.默认点击input输入框进行输入文本时候，会出现边框。应该在css样式设置为: 
        outline: none;
    2.input和button都是行内块，其父元素满足其宽度，但是还是不能同一行显示，考虑是其行内块之间的空格影响。
      可以使用float进行浮动。
  
  # 6.less中常用方法
    1.子代选择器:只是选择father的儿子son
    .father{
      &>.son{
        xxxx
      }
    }
    2.后带选择器：默认选择father的所有后代son
    .father{
      .son{
        xxxx
      }
    }
    3.交集选择器：两个都满足时候
    .father.mather{

    }


  # 7.绘制下拉框或者右侧框一般方法
     用li包裹a和div：当触及a标签时候显示隐藏div
     也就是：用一个大盒子div包裹两个部分，
     显示隐藏部分 和 点击部分 为兄弟关系。


# 8.伪类元素：after与before

  绘制盒子的下横线。
  .row::after {
        position: absolute;
        bottom: 0;
        left: 6px;
        content: "";
        width: 64px;
        height: 1px;
        background-color: #665e57;
      }

  绘制盒子的右竖线
  .col::before {
        position: absolute;
        right: 0;
        top: 6px;
        content: "";
        width: 1px;
        height: 64px;
        background-color: #665e57;
      }

  # 9. 针对图片跳转部分：
      一般设置为：外层一个a标签进行跳转，内层一个img存放图片。

  
  # 10.悬停到盒子上面：出现盒阴影，同时盒子网上走一走吗，如何做？
      
      // 设置鼠标触及动画
        &:hover {
          // 控制3d变换
          transform: translate3d(0, -2px, 0);
          // 控制盒子阴影
          box-shadow: 0 15px 30px rgba(0, 0, 0, .1);
        }

        学习动画！！！！！！！！！！！！
      
  # 11.为什么要清除浮动？？？？
  　　　
        1.清除浮动原因：当father父盒子不能设置高度时候，而子盒子却进行了float浮动，那么此时父盒子father的高度为0，会对father后续的盒子产生影响！也称为高度塌陷

        2.清除办法：

        ====> ①给父盒子设置高度height，使得浮动元素在盒子内部。
        
              缺点：网页制作中,高度height很少出现.为什么?因为能被内容撑高!父盒子的高度不是固定不变的。
        
        ====>  ②给父盒子添加：overflow：hidden或者auto
               但是仅仅适用于没有动画溢出或者阴影情况，否则对于动画或者阴影不能正常显示。

               缺点：overflow:hidden;的本意是将超出父类的部分隐藏，但是对于需要阴影或者translate动画的会成动画失效。

        
        ====>  ③使用 <div class="clear"></div>
                   .clear{clear:both;}

      　　　　1.如果father包含若干个浮动son元素，那么在father平级的后面添加一个带有clear类的盒子，可以是：div、br、hr。
        　　　　<div class="clear"></div>
        　　  2.然后再使用clear样式进行浮动清除。
        　　　　.clear{clear:both;}
            
            缺点：margin失效。
       
        ====> ④使用包含浮动元素的盒子添加伪元素方式清除浮动。
              <div class="vedio-box clear"></div>
              其中 类clear为：
              .clear::after {
                              content: "";
                              display: block;
                              clear: both;
                            }


  # 12.元素居中对齐？
     1.使用text-align进行水平对齐。
     2.使用lign-height进行垂直对齐。
     3.使用position的absolute进行绝对定位对齐。 必须显式声明外部容器元素的height
     4.使用margin进行居中对齐。  必须使用display: block

     5.flex布局
     6.translate居中
     7.grid布局。

  # 13.如何绘制一个椭圆？
     使用border-radius进行绘制：首先border-radius是形成一个半径为指定大小的圆，那么要绘制椭圆，只需要在短的那边设置为不足半径就可以。
     例如： 长 32 高 20 半径12
     那么：绘制出的椭圆就是长轴为32，短轴为20的椭圆。

     垂直方向圆的：半径取高度的一半
     水平方向圆的：半径取宽度的一半

  # 14.防止盒子内的内容溢出：
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    
  # 15.鼠标悬停出现下拉框如何实现？
  这样的下拉框：可以将鼠标滑动到该下拉框之中。
  用一个盒子a包裹盒子b，当触发a或者a的某一个子元素时候出现b。
  

  # 16.清除浮动；一般使用伪元素清除浮动
  .clear::after{
    content:"";
    dispaly:block;
    clear:both;
  }

  # 17.father使用relative，子元素使用absolute如何垂直水平居中？
     1.如果方便知道子元素的宽高，那么：
       ====> 子元素先设置 left top为父元素的50%
       ====> 子元素再设置margin值：
                    left为负的，值为子元素宽度的一半。
                    top为负的，值为子元素高度的一半。
       ====> eg:
            son {
                position: absolute;
                width: 100px;
                height: 50px;
                // 50%表示父元素的一半。
                left: 50%;
                top: 50%;
                // 再移动自己的一半，知道确切的宽度和高度条件。
                margin-left: -50px;
                margin-top: -25px;
              }  
      
    2.如果不知道子元素son的宽度和高度大小，使用transform。
        ====> 子元素先设置 left top为父元素的50%
        ====> 子元素在设置 transform向水平和竖直移动负值。
        ====> eg:
              son {
                  position: absolute;
                  // 50%表示窗口的一半。
                  left: 50%;
                  top: 50%;
                  // 再移动自己的一半，知道确切的宽度和高度条件。
                  transform: translate(-50%, -50%);
                }

  # 18.text-align对那些元素起作用？
      注意：行内块元素和行内元素都可以看成是父亲盒子中的文本，所以text-align可以使行内块元素和行内元素的盒子在父亲盒子中居中。

      块元素： h1-h6,p,div,ul,ol,li
      行内元素：a,span,strong,b,em,i,del,s,ins,u
      行内块级元素：img,input,td

  # 19.下拉框布局中遇到的问题-下拉框鼠标不能悬停

       1.问题描述：在使用father、son-btn、son-dropdown的格式进行设置下拉选择框时候，给father添加hover鼠标悬停之后，发现鼠标不能悬停到son-dropdown上面！

       2.问题原因：问题原因在于鼠标悬停是悬停在 father 元素之上的，而son-dropdown一般使用绝对定位进行位置定位，但是由于在定位过程中可能会造成son-dropdown与父盒子father之间存在间隙，同时绝对定位不占有初始位置，而鼠标只能在father的大小范围内进行悬停，因此会产生这样的原因。

       3.解决方法：根本原理：使father父盒子接壤son-dropdown绝对定位盒子。
                 
                 1.方法一-直接操作父盒子：给father足够大的宽度和高度，使得鼠标移动到son-dropdown时候依然在父盒子内部（相接即可！）
                 
                 2.方法二-操作btn子盒子：如果对son-dropdown盒子使用了margin-top或者绝对定位时候使用了top不为0，那么此时son-dropdown与father盒子已经分开了，需要将父盒子与son-dropdown盒子相接壤。
                 【为btn子盒子设置margin或者padding来撑大父盒子，使得父盒子能够接壤son-dropdown】
 
  # 20.子绝父相中如何实现 父元素的高度由子元素撑开？
    在实际开发中，父元素的宽度是由里面的子元素撑开的，而绝对定位的子元素由于脱离了父元素文本结构，所以是撑不开父元素的。不但撑不开，而且还会受到父元素宽度的限制。

    我们可以使用js解决：选择子元素的宽度赋值给父元素宽度。
    <script>
      document.querySelector('#father').style.height = document.querySelector('#child').offsetHeight + margin + padding +'px';
    </script>

# 21.father中img如何与son-div进行水平居中对齐？
    1.首先对father使用： text-align进行center、line-height=height进行元素水平垂直居中

    2.将右侧的son-div转变为 display: inline-block;
    
    3.对son-div施加：vertical-align：midule