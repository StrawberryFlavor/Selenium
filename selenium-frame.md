**明明元素就在那，firebug也可以看到，但是无论怎么定位还是定位不到的时候，需要检查下页面是否含有iframe，你需要定位的元素是否在iframe之中，有可能就是因为iframe的问题。在一个default content中查找一个在iframe 中的元素，那肯定是找不到，同样你在一个iframe 中查找另一个iframe元素或default content中的元素，那必然也定位不到**

### 切换到frame之中 ###
selenium提供了switch_to_frame()方法来切换frame，
如
```py
driver.switch_to.frame(reference)
```
<!-- more -->
reference是传入的参数，用来定位frame，可以传入id、name、index以及selenium的WebElement对象

>reference一般输id，但是也有动态id的情况，可以使用xpath定位，然后传入WebElement对象

### 从frame之中切换到default content主文档 ###
切换进入frame之中后，我们就不能对主文档的元素进行操作了，如果需要操作，那么我们只能再切换回去

```py
driver.switch_to.default_content()
```
### 遇到嵌套的frame ###
遇到嵌套的frame的时候，也就是一个frame里面还有一个frame的时候，我们要一层一层切换进去，如

```py
driver.switch_to.frame("frame1")   
```

```py                          
driver.switch_to.frame("frame2")
```

如果我们已经切换到frame2中，那么我们要返回frame之中怎么办。selenium为我们提供了一个后退的方法。

```py
driver.switch_to.parent_frame()
```

如果当前已经是主文档了，那么后退没有效果