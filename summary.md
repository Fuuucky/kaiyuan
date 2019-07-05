# 国际双创实践周 - 开源硬件实战

## 一. 国际双创实践周参与情况

### 第一天

介绍了 Arduino 硬件, 创客思想

介绍了 Arduino IDE, Processing , fritzing

介绍了 Github


作业:

安装三个软件

![](./assets/arduino.png)

![](./assets/processing.png)

![](./assets/frizting.png)

注册GitHub 建立仓库用于提交编程作业

### 第二天

讲解了Arduino 基础编程, 串口编程

作业:

在Arduino上完成, 从电脑串口接收一串字符, 使用LED 发送对应的Morse码



![](./morse_day4/circuit.png)



### 第三天

介绍了Arduino仿真网站 Tinkercad

讲解了电机的使用, PWM技术

讲解了7段数码管编程, CD4511使用

作业:

在Arduino上完成

给课堂例子增加转向灯功能

![](./day3/classwork/circuit.png)

通过串口输入数字, 在数码管显示

![1562291407105](./day3/homework/circuit.png)

```c++
char num;

void setup(){
    Serial.begin(9600);
  	for(char i = 2; i < 6; i++)
      pinMode(i, OUTPUT);
}

void loop(){
	while(Serial.available() > 0){
      num = Serial.read() ;
      if(isDigit(num)){
        num -= '0';
      	for(char i = 0; i < 4; i++)
          digitalWrite(i + 2, (num>>i) & 1u);
      }
    }
    delay(10);
}
```

### 第四天

以仿真方式完善第一天内容

答疑环节

交流和总结

作业:

撰写总结报告

完善Github仓库格式


![](./morse_day4/circuit.png)

```c++
#define DEBUG

class MorseBase {
  int _pin;
  const int clk = 250;

public:
  MorseBase(int8_t pin) : _pin(pin) { pinMode(pin, OUTPUT); }
  inline void dit() {
    digitalWrite(_pin, HIGH);
    delay(clk);
    digitalWrite(_pin, LOW);
    delay(clk);
#ifdef DEBUG
    Serial.print('.');
#endif
  }
  inline void dah() {
    digitalWrite(_pin, HIGH);
    delay(clk * 3);
    digitalWrite(_pin, LOW);
    delay(clk);
#ifdef DEBUG
    Serial.print('-');
#endif
  }
  inline void eoc() {
    delay(clk << 1);
#ifdef DEBUG
    Serial.print(' ');
#endif
  }
  inline void eow() {
    delay((clk << 2) + (clk << 1));
#ifdef DEBUG
    Serial.print("/");
#endif
  }
};

MorseBase x(13);

bool isInitial = true;
char ch = 0;

void setup() { Serial.begin(9600); }

void loop() {
  if (Serial.available() > 0) {
    ch = Serial.read();
    if (isUpperCase(ch))
      ch |= 0x20u;
    if (isInitial)
      isInitial = false;
    else if (ch != ' ')
      x.eoc();
    else {
      isInitial = true;
      x.eow();
    }
    switch (ch) {
      case 'a': x.dit(); x.dah(); break;
      case 'b': x.dah(); x.dit(); x.dit(); x.dit(); break;
      case 'c': x.dah(); x.dit(); x.dah(); x.dit(); break;
      case 'd': x.dah(); x.dit(); x.dit(); break;
      case 'e': x.dit(); break;
      case 'f': x.dit(); x.dit(); x.dah(); x.dit(); break;
      case 'g': x.dah(); x.dah(); x.dit(); break;
      case 'h': x.dit(); x.dit(); x.dit(); x.dit(); break;
      case 'i': x.dit(); x.dit(); break;
      case 'j': x.dit(); x.dah(); x.dah(); x.dah(); break;
      case 'k': x.dah(); x.dit(); x.dah(); break;
      case 'l': x.dit(); x.dah(); x.dit(); x.dit(); break;
      case 'm': x.dah(); x.dah(); break;
      case 'n': x.dah(); x.dit(); break;
      case 'o': x.dah(); x.dah(); x.dah(); break;
      case 'p': x.dit(); x.dah(); x.dah(); x.dit(); break;
      case 'q': x.dah(); x.dah(); x.dit(); x.dah(); break;
      case 'r': x.dit(); x.dah(); x.dit(); break;
      case 's': x.dit(); x.dit(); x.dit(); x.dit(); break;
      case 't': x.dah(); break;
      case 'u': x.dit(); x.dit(); x.dah(); break;
      case 'v': x.dit(); x.dit(); x.dit(); x.dah(); break;
      case 'w': x.dit(); x.dah(); x.dah(); break;
      case 'x': x.dah(); x.dit(); x.dit(); x.dah(); break;
      case 'y': x.dah(); x.dit(); x.dah(); x.dah(); break;
      case 'z': x.dah(); x.dah(); x.dit(); x.dit(); break;
      case '0': x.dah(); x.dah(); x.dah(); x.dah(); x.dah(); break;
      case '1': x.dit(); x.dah(); x.dah(); x.dah(); x.dah(); break;
      case '2': x.dit(); x.dit(); x.dah(); x.dah(); x.dah(); break;
      case '3': x.dit(); x.dit(); x.dit(); x.dah(); x.dah(); break;
      case '4': x.dit(); x.dit(); x.dit(); x.dit(); x.dah(); break;
      case '5': x.dit(); x.dit(); x.dit(); x.dit(); x.dit(); break;
      case '6': x.dah(); x.dit(); x.dit(); x.dit(); x.dit(); break;
      case '7': x.dah(); x.dah(); x.dit(); x.dit(); x.dit(); break;
      case '8': x.dah(); x.dah(); x.dah(); x.dit(); x.dit(); break;
      case '9': x.dah(); x.dah(); x.dah(); x.dah(); x.dit(); break;
      case ',': x.dah(); x.dah(); x.dit(); x.dit(); x.dah(); x.dah(); break;
      case '.': x.dit(); x.dah(); x.dit(); x.dah(); x.dit(); x.dah(); break;
      case '?': x.dit(); x.dit(); x.dah(); x.dah(); x.dit(); x.dit(); break;
      case '!': x.dit(); x.dit(); x.dah(); x.dah(); x.dit(); break;
      case '\"': x.dit(); x.dah(); x.dit(); x.dit(); x.dah(); x.dit(); break;
      case '\'': x.dit(); x.dah(); x.dah(); x.dah(); x.dah(); x.dit(); break;
      case '-': x.dah(); x.dit(); x.dit();x.dit(); x.dit(); x.dah(); break;
    }
  }
}
```

## 二. 国际双创实验周主要收获

学习到了Arduino 的基础入门知识

在老师的指导下完成了多次实验

体会到了 使用Arduino创造的快乐

增加了对开源硬件的兴趣

## 三. 意见与建议

学校应对每一门双创周课程标明其前置课程

避免没有基础或基础不过关的同学影响教学进度

对于此门课程， 老师的讲解是过关的

但是由于面向了大一同学开课

很多内容都没有办法开展

包括 基础的Linux使用， git的使用，数字电路相关内容，

甚至 C++ 的基础 都要老师去现场讲解

这极大程度的拖慢了教学进度， 使得课程达不到预期效果

对于大二同学来说， 很多计算机相关的基础知识都是不过关的

侧面反映了我校本科生计算机教学出现的一些问题：

包括 专业课脱离实践， 知识深度不够， 学生技能不过关等问题