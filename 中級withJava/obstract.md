```java
//緯度によって、northかsouthかを返す関数
//Stringデータを受け取って、double型を返す。
double getLatitudeOfCity(String cityString)

//関数から帰ってくる値が、doubleだから、こういう書き方ができる。
if (getLatitudeOfCity("Las Vegas") > 0) message += "north";
```
