* 当想要输出 % 时，可以通过 printf("%%")实现	

*  != 的运算优先级要比 = 的运算优先级要高

* 练习 1 - 6 验证表达式getchar != EOF的值是0还是1

  ```c++
  #include <stdio.h>
  
  int main()
  {
      int c = getchar();
      do {
          if(c == EOF) {
              printf("this is EOF\n");
          }
      }while(c = getchar());
      return 0;
  }
  ```

* 练习 1 - 7 编写一个打印EOF值的程序

  ```c++
  #include <bits/stdc++.h>
  using namespace std;
  int main()
  {
    int c;
    c = getchar();
    
    do 
    {
      putchar(c);
      c = getchar();
      if(c == EOF) {
        printf("the value of EOF is %d\n", c);
      }
    }while(c != EOF);
  
    return 0;
  }
  
  // ctrl + z
  //the value of EOF is -1
  ```

* 编写一个将输入复制到输出的程序，并将其中连续的多个空格用一个空格代替

  ```c++
  #include <stdio.h>
  int main()
  {
      int flag = 0;
      int c;
      while((c = getchar()) != EOF) 
      {
      	if(c == ' ')
          {
              if(flag) continue;
                flag = 1;
              putchar();
          }
          else {
             flag = 0;
             putchar();
          }
      }
      return 0;
  }
  ```

* 编写一个将输入复制到输出的程序，并将其中的制表符替换为\t, 将会退辅替换为\b， 将反斜杠替换为 \\\, 这样可以将制表符和回退符通过可见的方式显示出来

  ```c++
  #include <bits/stdc++.h>
  using namespace std;
  int main()
  {
    int c;
  
    while((c = getchar()) != EOF) 
    {
      if(c == '\t') 
      {
        putchar('\\');
        putchar('t');
      }
      else if(c == '\\') 
      {
        putchar('\\');                                                                                                                             
        putchar('\\');
      }
  
      else if(c == '\b')
      {
        putchar('\\');
        putchar('b');
      }   
    }
    return 0;
  }
  
  ```

  