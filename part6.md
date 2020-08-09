第六章 结构

* 如果传递给函数的结构很大，使用指针方式的效率通常比复制整个结构的效率要高。

  ```c++
  struct point *pp;
  ```

  可以使用如下的方式使用pp。

  ```c++
  struct point origin, *pp;
  pp = &origin;
  printf("%d %d\n", (*pp).x, (*pp.y));
  // 或者是如下的方法
  printf("%d %d\n", pp->x, pp->y);
  ```

  注意圆括号是必须要加的，因为结构成员运算符 “.” 的优先级要比 "*" 的优先级高 

  ```c++
  *pp.x 
  //等价于
  *(pp.x)
  ```

* 为了表示方便，C语言提供了另一种简写方式。

  ```c++
  struct rect r, *rp = &r;
  // 运算符 . 和 -> 都是从左至右结合的
  //以下四个表达式时等价的
  r.pt1.x
  rp->pt1.x
  (r.pt1).x
  (rp->pt1).x
  ```

* 小对比

  ```c++
  struct point origin, *pp;
  pp = &origin;
  
  struct point origin, *pp;
  *pp = &origin;
  
  struct point origin, *pp = &origin;
  ```

  ~~第一种情况pp存储的是origin的地址，当调用*pp时，\*pp的值就是origin这个对象~~

  ~~第二种情况*pp存储的是origin的地址~~

* 在所有的运算符中，下面四个运算符的优先级最高，结构运算符 "."和 "->" ，由于函数调用 "()"以及用于下标的 "[]" 。因此，他们同操作数之间的结合也是最紧密的。

  ```c++
  ++p->len
  // 等价于 ++(p->len)
  *p->str
  // 等价于 *(p->str)
  *p->str++
  // 先读取指针str指向的对象的是，然后+1，然后再读取对应的操作
  (*p->str)++
  // 将指针str指向的对象的值+1
  *p++->str
  // 先读取指针的值，然后再+1
  ```

  