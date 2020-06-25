# การทำระบบ Monitor Server * MySQL ง่าย ๆ ด้วย Docker (grafana + prometheus + node exportor + mysql exportor)
## คู่มือนี้ มี 2 แบบ 
1. ใช้ไปเลย บ่อยากเข้าใจหยัง
2. มันเฮ็ดงานจั่งใด๋วะ

### คู่มือแบบที่ 1

    git clone https://github.com/cybernude/server-monitor.git
    cd server-monitor
    
#### จากนั้น ทำการแก้ไขทำการแก้ไขไฟล์  docker-compose.yml ด้วย editor ที่ถนัด
แก้ไขค่าการเชื่อมต่อ database ของเรา จะอยู่ประมาณบรรทัดที่ 12

    - "DATA_SOURCE_NAME=root:123456@(10.0.0.181:3333)/"


    root = user ของฐานข้อมูล
    123456 = password ของฐานข้อมูล
    10.0.0.181 = ip ของฐานข้อมูล
    3333 = port ที่เชื่อมต่อ database ของเรา

แก้แค่นี้แหละครับ จากนั้น save ครับ

[![2020-06-25-7-18-52.png](https://i.postimg.cc/s2xQY8s7/2020-06-25-7-18-52.png)](https://postimg.cc/hJFtg2Jt)

#### จากนั้นทดสอบ ว่ามันทำงานได้ไหม

    docker-compose up

จะเจอหน้าจอดำ ๆ กะข้อความอิหยังบุ๊ แหล่นล้าย ๆ ประมาณนี้

[![2020-06-25-7-25-00.png](https://i.postimg.cc/cLH42n2N/2020-06-25-7-25-00.png)](https://postimg.cc/crpS8rdD)


จากนั้นนั้น เปิด browser ที่เราถนัด ใส่ url = http://ip_server:3000

    ip_server = ip ของ server ที่เราติดตั้งตัว server monitor นี้

จะเจอหน้าจอ login
    
    user = admin
    password = admin
    
จากนั้น เลือกกราฟ ที่จะเราจะ monitor ครับ ผมใส่มาให้แล้ว 2 กราฟคือ
1. MySQL Overview สำหรับการ monitor mysql server ของเราครับ
2. Node Exporter Full ไว้สำหรับ monitor ตัวเครื่อง server ของเราครับ

การเลือกแสดงกราฟ ครั้งแรก ไปที่ 

    เครื่องหมายแว่นขยาย ---> Search

[![2020-06-25-7-47-10.png](https://i.postimg.cc/66b9R3Tj/2020-06-25-7-47-10.png)](https://postimg.cc/9zT5HcdZ)


จะเจอกราฟสองกราฟ ที่ว่าด้านบนครับ เลือกกดดูได้เลย (ครั้งต่อ ๆ ไป เรา Login เข้ามา มันจะอยู่ที่หน้าแรกเลย)

[![2020-06-25-7-32-33.png](https://i.postimg.cc/MZdC4FSv/2020-06-25-7-32-33.png)](https://postimg.cc/0rKXKZrs)


เข้าไปดูแรก ๆ อาจจะ ไม่เห็นอะไรขยับ ไม่ต้องตกใจ ให้ไปเปลี่ยน Time Rang ของมันก่อน อยู่ที มุมขวาบน ตรงคำว่า

    ถ้าเป็น Mysql Overview = Last 12 Hours
    ถ้าเป็น Node Exportor Full = Last 24 House

เลือกเป็น Last 5 Minutes ก็ได้ครับ จะได้มองเห็นว่ามันขยับ

[![2020-06-25-7-49-42.png](https://i.postimg.cc/TYWXDJz1/2020-06-25-7-49-42.png)](https://postimg.cc/N5YVhmfv)

[![2020-06-25-7-49-12.png](https://i.postimg.cc/3RwsJXjK/2020-06-25-7-49-12.png)](https://postimg.cc/PLB3S8Fc)

ถ้ากราฟ ทั้งสองตัว ทำงานได้ ถูกต้อง ก็เรียบร้อย ยินดีด้วยครับ คุณได้ ระบบ Monitor Server แบบชิว ๆ แล้ว ให้เรากลับมาที่หน้าจอ Console ที่เราเปิดค้างไว้ตะกี๊ (ที่มีข้อความแหล่น ล้าย ๆ นั่นหล่ะ) จากนั้นกด 

    Ctrl + c

เพื่อออกจากการรัน docker-compose up ครับ เพราะถ้ารันแบบนี้ มันจะค้างหน้าจอแบบนี้อยู่ อันนี้เราทดสอบรันเพื่อเช็คว่ามันทำงานได้ถูกต้องไหมครับ จากนั้นสั่ง ให้ระบบมันรันอีกรอบ แต่ให้มันรันเป็น daemon อยู่เบื้องหลังด้วยคำสั่ง

    docker-compose up -d

จากนั้น ลองเรียกใช้งานอีกทีครับผม

##### เสร็จเรียบร้อย แล้ว เล่าให้ยืดยาวเฉย ๆ หลัก ๆ มีแค่แก้ config การเชื่อมต่อ database ของเราเฉย ๆ กระบวนการทั้งหมดนี้ ถ้าอ่าน ทำความเข้าใจ ก่อนเริ่มลงมือทำ ใช้เวลา ไม่ถึง 5 นาที เราก็มีระบบ Monitor Server ดี ๆ ไว้ใช้แล้วครับ

##### จบ คู่มือ แบบ ที่ 1


