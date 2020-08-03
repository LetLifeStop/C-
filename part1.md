**字符在及其内容是通过位模式存储的，char类型专门用于存储这种字符型数据，当然任何整形也可以用于存储字符型数据，由于某些潜在的重要原因，我们再次使用int**

​	~~这个 潜在的重要原因 现在不知道，等后续补充~~



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
  // the value of EOF is -1
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
  
* 编写一个程序，以每行一个单词的形式打印其输入

  ```c++
  #include <bits/stdc++.h>
  using namespace std;
  int main()
  {
    int c;
  
    while((c = getchar()) != EOF) 
    {
      if(c == ' ' || c == '\n')
      {
        putchar('\n');
        continue;
      }
      putchar(c);
    }
    return 0;
  }      
  ```

* 对于函数的参数，在C语言中传递给被调用函数的参数的值存放在临时变量中，而不是存放在原来的变量中。这样设置的作用即有利又有弊，缺点就是耗费空间，优点就是在某些情况下可以减少变量的申请。

  ```c++
  int pow(int base, int n) 
  {
    int p;
    
    for(p = 1; n > 0; --n)
        p = p * n;
   
    return p;
  }
  ```

  比如上面的例子，对n的操作不会影响到原来n的值。

  如果要修改函数参数中对应的值，可以将原来变量的地址作为参数进行传入，函数要将对应的参数声明为指针类型 **从技术角度看，地址就是指向变量的指针**

* 对于参数为数组时，传递给函数的是数组的起始位置，并不会复制数组本身

* 练习：程序读入一组文本行，并把最长的文本行打印出来 

  

  ```c++
  // 封装getline函数，getline通过getchar实现
  // 自己的版本
    #include <stdio.h>
    #define MAXLINE 100 
    
    void Getline(int c, char tmpSto[], char longest[]); 
    void copy(char src[], char dst[], int len);
    
    int main()
    {
      int c;
      char tmpSto[MAXLINE];
      char longest[MAXLINE];
    
      Getline(c, tmpSto, longest);
      
      printf("the longest str is %s\n", longest);
      return 0;
    }
    
    void Getline(int c, char tmpSto[], char longest[])
    {
      int max_len = 0, len = 0;
    
      while((c = getchar()) != EOF) {
        tmpSto[len++] = c;
        if(c == '\n') 
        {   
          if(len > max_len) 
          {
            max_len = len;
            copy(tmpSto, longest, len);
          }
          len = 0;
        }
      }
      
      return ;
    }
    
    void copy(char src[], char dst[], int len) 
    {
      for(int i = 0; i < len; i++) 
      {
        dst[i] = src[i];
      }                                                                                     
      dst[len] = '\0';
      printf("the dst is %s\n", dst);
      return ;
    }
  ```

  看了样例之后的改进版

  ```c++
  #include <stdio.h>
    #define MAXLINE 100 
    
    void Getline(int c, char tmpSto[], char longest[]); 
    void copy(char src[], char dst[], int len);
    
    int main()
    {
      int c;
      char tmpSto[MAXLINE];
      char longest[MAXLINE];
    
     Getline(c, tmpSto, longest);
      
      printf("the longest str is %s\n", longest);
      return 0;
    }
    
    void Getline(int c, char tmpSto[], char longest[])
    {
      int max_len = 0, len = 0;
    
      while((c = getchar()) != EOF) {
        tmpSto[len++] = c;
        if(c == '\n') 
        {
          tmpSto[len] = '\0';
          if(len > max_len) 
          {
            max_len = len;
            copy(tmpSto, longest, len);
          }
          len = 0;
        }
      }
      
      return ;
    }
    
   void copy(char src[], char dst[], int len) 
    {
      int i = 0;
      while((dst[i] = src[i]) != '\0')                               
        i++;
      return ;
    }  
  ```

* 对比一下，在获得一个完整的行之后，忘记在Getline函数中加行终止符。 在copy函数中，可以写的更加简便一点

* getline函数把字符'\0' [空字符，其值为0]，插入到它创建的数组末尾，用来标记字符串的结束，这是C语言的一个约定

* **对于上面的getline函数，还有一个可以再去考虑的地方**

  ```c++
  void Getline(int c, char tmpSto[], char longest[])
    {
      int max_len = 0, len = 0;
    
      while((c = getchar()) != EOF && len < limit/*limit参数可以作为函数参数再次加入*/) {
        tmpSto[len++] = c;
        if(c == '\n') 
        {
          tmpSto[len] = '\0';
          if(len > max_len) 
          {
            max_len = len;
            copy(tmpSto, longest, len);
          }
          len = 0;
        }
      }
      
      return ;
    }
  ```

  **更新了这个之后，getline函数当数组满时，将停止读取字符**
  
* 编写函数reverse(s). 将字符串s中的字符顺序颠倒过来。使用该函数编写一个程序，每次颠倒一个输入行中的字符顺序

  ```c++
  #include <stdio.h>
  #define MAXLINE 100 
    
  void reverse(char str[]);
  void Swap(char *t1, char *t2);
    
  int main()
  {    
    char str[MAXLINE];
      
    scanf("%s", str);
    reverse(str);
      
    printf("the reverse str is %s\n", str);
    return 0;                                             
  }
    
  void reverse(char str[]) 
    
    int i, len = 0;
      
    while(str[len] != '\0')
    {
      len++;
    }
    printf("the length of str is %d\n", ln) 
    printf("1------%s\n", str);
    for(i = 0; i < len / 2; i++) 
    {
      Swap(&str[i], &str[len - (i + 1)]);
    }
    printf("1------%s\n", str);
   
     return ;
  }
  
  void Swap(char *t1, char *t2)
  {
    char tmp;
    tmp = *t1;
    *t1 = *t2;
    *t2 = tmp;
    return ;
  }
  ```

* "定义" 表示创建变量或者分配存储单元，"声明"代表说明变量的性质，但是并不分配存储单元

* 过分依赖外部变量会导致一定的风险，因为他会使得程序中的数据关系模糊不清**(外部变量的值可能会被意外的或者不经意地修改)**

* 定义表示创建变量或者分配存储单元，而声明指的是说明变量的性质，但是并不分配存储单元

* 过分依赖外部变量会导致一定的风险，因为它会使程序中的数据关系模糊不清{外部变量的值可能会被以外的或者不经意的修改}

* 编写一个程序，删除C语言程序中所有的注释语句，要正确的处理带引号的字符串和字符常量，在C语言中，注释不允许嵌套

  ```c++
    #include <stdio.h>
    #include <string.h>
    # define MAXLINE 1000
    
    void Erase(char str[]);
    
    int main()
    {
      
      char acStr[MAXLINE];
    
      for(int i = 0; (acStr[i] = getchar()) != EOF; i++); 
    
      Erase(acStr);
      puts(acStr);
      return 0;
    }                                                                                                                          
    
    void Erase(char acStr[])
    {
      int len = strlen(acStr);
      int j, pos, flag = 0;
    
      for(int i = 0; i < len; i++)
      {
        if(acStr[i] == '"')
          flag++;
        if(flag % 2 == 0 && acStr[i] == '/' && i + 1 < len && acStr[i + 1] == '/')
        {   
          for(j = i; j < len && acStr[j] != '\n'; j++) 
          {   
            acStr[j] = ' ';
          }   
          i = j;
        }   
        if(flag % 2 == 0 && acStr[i] == '/' && i + 1 < len && acStr[i + 1] == '*')
        {   
          for(j = i + 1; j < len ; j++)  
          {   
            // printf("the pos is %d, the acstr[j] is %u\n", i, acStr[j]);
            if(acStr[j] == '*' && j + 1 < len && acStr[j + 1] == '/')
            {   
              acStr[j + 1] = ' ';
              break;
            }   
            acStr[j] = ' ';
          }   
          acStr[i] = ' ';
          acStr[j] = ' ';
          i = j + 2;
        }   
      }
      return ;
    }
  ```

  