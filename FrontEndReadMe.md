# วิธีตั้งค่าสำหรับ FrontEnd Developer
## การวางไฟล์ SASS / SCSS
บริษัทฯเชื่อว่าซอฟต์แวร์คุณภาพเริ่มต้นจากโค๊ดที่เขียนขึ้นตามฟอร์แม่ทมาตรฐานสากล บริษัทฯใช้ GitLab ในการทำ Automated Testing เบื้องต้นในการลดภาระของ Software Tester ของบริษัทฯ และเป็นการช่วย Developer ในการตรวจสอบผลลัพธ์ก่อนส่งมอบงานได้แบบ Real Time โดยเข้าไปที่ `https://<project_name>.durian.software`

- กรุณาเก็บ SASS / SCSS SourceCode ของคุณใว้ที่ `resources/assets/BackOffice/<project_name>/<RESTful_action>.scss`
- ตั้งค่า Webpack สำหรับการ compile บนเซิร์ฟเวอร์ได้ที่ไฟล์ `webpack.mix.js` (ข้อมูลเพิ่มเติม และวิธีตั้งค่า Mix [คลิ๊ก](https://laravel.com/docs/master/mix))

## การวางไฟล์ JavaScript
เช่นเดียวกับ SASS / SCSS บริษัทฯใช้ GitLab ในการทำ Automated Testing เบื้องต้นในการลดภาระของ Software Tester ของบริษัทฯ และเป็นการช่วย Developer ในการตรวจสอบผลลัพธ์ก่อนส่งมอบงานได้แบบ Real Time

- กรุณาเก็บ Source Code ใว้ที่ `resources/assets/js/BackOffice/<project_name>/<RESTful_action>.js`
- ตั้งค่า Webpack สำหรับการ compile บนเซิร์ฟเวอร์ได้ที่ไฟล์ `webpack.mix.js`

## Corporate Identity (CI)
เพื่อให้การใช้สี ฟอนต์ ปุ่ม ช่องว่างระหว่าง component และอื่นๆ เป็นไปตาม Corporate Identity (CI) ที่ Designer ของบริษัทฯได้วางใว้ เจ้าหน้าที่ของบริษัทฯได้ทำปรับแต่งค่าของ CSS กลางใว้ให้แล้วซึ่ง FrontEnd Developer สามารถดูข้อมูลการตั้งค่าต่างๆได้จากไฟล์ CSS หลัก `sass/app.scss` หาก Developer มีความประสงค์จะปรับแต่งค่าของ CSS กลางนี้ ขอความกรุณาติดต่อที่เจ้าหน้าที่ผ่าน [FaceBook Pages](https://www.facebook/adiwitcoth)

## การวาง Routes
เราใช้ไฟล์ `routes/web.php` เพื่อ redirect URL จาก Browser ไปยังโมดูลปลายทางที่ถูกต้อง โปรดอย่าแก้ไขไฟล์นี้เพื่อป้องกันไม่ให้ส่งผลกระทบต่อ Developer ท่านอื่น ๆ ทั้งนี้หาก Developer มีความประสงค์จะปรับแต่งค่าของ Routes นี้ ขอความกรุณาติดต่อที่เจ้าหน้าที่ผ่าน [FaceBook Pages](https://www.facebook/adiwitcoth)

## การพัฒนา MockUp
เพื่อให้ Developer สามารถโฟกัสในการพัฒนา MockUp แต่ละหน้า เจ้าหน้าที่ของบริษัทฯได้ทำการตั้งค่าในส่วนของ Header, Footer และ Sidebar (ถ้ามี) ให้กับ Developer เรียบร้อยแล้วใว้ที่ไฟล์ `layouts/html5.blade.php`

โดย Developer แก้ไขในไฟล์ของตัวเองที่ `resources/view/BackOffice/<project_name>/<RESTful_action>.blade.php` สามารถเพิ่มไฟล์ในส่วนสำคัญต่างๆของหน้าได้ผ่าน section ที่เจ้าหน้าที่ของบริษัทฯได้เจาะใว้ให้ ดังนี้:

โค๊ดพิเศษที่ต้องการใส่เพิ่มเติมในส่วนของ `<head></head>` เช่น `<link>`, `<meta>`, `<title>` หรืออื่นๆ Developer สามารถใส่เพิ่มเติมได้ตามต้องการที่

```
@section('head')
    <link rel="stylesheet" href="{{ asset('css/<project_name>/<RESTful_action>.css') }}">
    <meta name="author" content="John Doe">
    <style>
        body {background-color: orange;}
    </style>
@endsection
```

โค๊ด `<script></script>` พิเศษที่ต้องการใส่เพิ่มเติมก่อนปิด `</body>` Developer สามารถใส่เพิ่มเติมได้ตามต้องการที่

```
@section('script')
    <script>
        function myFunction {
            document.getElementById("demo").innerHTML = "Hello JavaScript!";
        }
    </script>
    <script src="{{ asset('js/<project_name>/<RESTful_action>.js') }}">
@endsection
```

และสำหรับโค๊ด HTML ของหน้า

```
@section('body`)
    <div class="container-fluid">
    </div>
@endsection
```

## การ Compile งาน SaSS และ JavaScript
เช่นเดียวกับการพัฒนา MockUp โดยใช้ HTML ตามปกติ, Developer สามารถใช้ NPM หรือ YARN ในการ compile ไฟล์ SASS / SCSS / JavaScript ได้โดย `cd user` เข้าไปยังโฟลเดอร์ที่เก็บโค๊ดโปรแกรมของคุณ แล้วใช้คำสั่ง `npm run dev` หรือ `yarn run dev` แล้วเปิดดูผลงานของคุณผ่าน browser ที่ URL (http://localhost)