---
layout: post
title: "Error compiling Amarino with Arduino 1.0"
date: 2011-12-08 15:12
comments: true
categories: Arduino
tags: Arduino
---

##[New MeetAndroid][NM] has been released to work with Arduino 1.0

[NM]:http://code.google.com/p/amarino/downloads/detail?name=MeetAndroid_4.zip&can=2&q=

*Chinese version below*

<!--more-->

## Amarino Compatibility issue when upgrading to Arduino 1.0

You need meetAndroid library to use the Amarino.

When you upgrade your Arduino to version 1.0, you may encounter compile errors while using [
meetAndroid][MA].

[MA]: http://code.google.com/p/amarino/


### Error Message 1 

```
/Applications/Arduino.app/Contents/Resources/Java/libraries/MeetAndroid/MeetAndroid.h:104: error: conflicting return type specified for 'virtual void MeetAndroid::write(uint8_t)'

/Applications/Arduino.app/Contents/Resources/Java/hardware/arduino/cores/arduino/Print.h:48: error:   overriding 'virtual size_t Print::write(uint8_t)'
```

#### Solution

According to the release notes from [Arduino][ar]

<blockquote>
The write(), print(), and println() functions in Stream now return a size_t (instead of void). This indicates the number of bytes actually written by the function. Any classes that inherit from Stream will need to change accordingly. Additionally the write(str) function has been given a concrete implementation – it calls write(buf, len) - so sub-classes don't need to (and shouldn't) implement it.
</blockquote>

[ar]: http://arduino.cc/en/Main/ReleaseNotes

Change return type of write function 

*in MeetAndroid.cpp line 263*

``` cpp
void MeetAndroid::write(uint8_t b){
	Serial.print(b);
}
```

to

``` cpp
size_t MeetAndroid::write(uint8_t b){
	Serial.print(b);
}
```

*in MeetAndroid.h line 104*

``` cpp
void write(uint8_t);
```

to

``` cpp
size_t write(uint8_t);
```

Compile again, Then you may get this error:

### Error Message 2

```
/Applications/Arduino.app/Contents/Resources/Java/libraries/MeetAndroid/MeetAndroid.cpp:21:22: error: WProgram.h: No such file or directory

/Applications/Arduino.app/Contents/Resources/Java/libraries/MeetAndroid/MeetAndroid.cpp:23:24: error: WConstants.h: No such file or directory
```

#### Solution

According to the release notes from [Arduino][ar2]
[ar2]: http://arduino.cc/en/Main/ReleaseNotes

<blockquote>
The WProgram.h file, which provides declarations for the Arduino API, has been renamed to Arduino.h.
</blockquote>

 To create a library that will work in both Arduino 0022 and Arduino 1.0, you can use an #ifdef that checks for the ARDUINO constant, which was 22 and is now 100.  For example:

``` cpp
#if defined(ARDUINO) && ARDUINO >= 100
#include "Arduino.h"
#else
#include "WProgram.h"
#endif
```

Comments WProgram.h & WConstants.h and add the code above

*in MeetAndroid.cpp line 21*

``` cpp
#include "WProgram.h"
#include "WConstants.h"
```

to

``` cpp
//#include "WProgram.h"
//#include "WConstants.h"
#if defined(ARDUINO) && ARDUINO >= 100
#include "Arduino.h"
#else
#include "WProgram.h"
#include "WConstants.h"
#endif
```

That's it. You should be good to use Amarino with Arduino version 1.0 now.





## 升級 Arduino 1.0 使用 Amarino 會碰到的問題

根據[官方文件][Q]，現在write()函式回傳型別為size_t，
[Q]: http://arduino.cc/en/Main/ReleaseNotes

修改MeetAndroid.cpp & MeetAndroid.h

*in MeetAndroid.cpp 263 行*

``` cpp
void MeetAndroid::write(uint8_t b){
	Serial.print(b);
}
```

改為

``` cpp
size_t MeetAndroid::write(uint8_t b){
	Serial.print(b);
}
```

*in MeetAndroid.h 104 行*

``` cpp
void write(uint8_t);
```

改為

``` cpp
size_t write(uint8_t);
```

根據[官方文件][R]，WProgram.h現在改為Arduino.h。
[R]:http://arduino.cc/en/Main/ReleaseNotes

修改 MeetAndroid.cpp

*in MeetAndroid.cpp 21 行*    

``` cpp
#include "WProgram.h"
#include "WConstants.h"
```

to
    
``` cpp
//#include "WProgram.h"
//#include "WConstants.h"
#if defined(ARDUINO) && ARDUINO >= 100
#include "Arduino.h"
#else
#include "WProgram.h"
#include "WConstants.h"
#endif
```

你也可以直接刪除 WProgram.h 跟 WConstants.h
加入 `#include "Arduino.h"` 即可。    
上面的作法是讓 Arduino 0022 跟 version 1.0 都可以使用Amarino。
