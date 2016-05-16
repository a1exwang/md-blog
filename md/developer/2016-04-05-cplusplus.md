# C++ "Interesting" Parts

- c++, cpp, cplusplus

------

1. 构造函数
  - 尽量在构造函数中只做赋值型的初始化

    ```
    AlexSubtarget::AlexSubtarget(xx tt, xx cpu, xx fs, xx tm) :
        AlexGenSubtargetInfo(tt, cpu, fs), // superclass
        registerInfo(new AlexRegisterInfo(this)),
        targetLowering(new AlexTargetLowering(tm, this))
    ```

    其中AlexTargetLowering的构造函数中使用了AlexSubtarget的getRegisterInfo(),
  获取了registerInfo对象, 但是此时registerInfo还没初始化
