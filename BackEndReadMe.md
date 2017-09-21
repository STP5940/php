# วิธีตั้งค่าสำหรับ BackEnd Developer
เราใช้ไฟล์ `routes/web.php` เพื่อ redirect URL จาก Browser ไปยังโมดูลปลายทางที่ถูกต้อง โปรดอย่าแก้ไขไฟล์นี้เพื่อป้องกันไม่ให้ส่งผลกระทบต่อ Developer ท่านอื่น ๆ ทั้งนี้หาก Developer มีความประสงค์จะปรับแต่งค่าของ Routes นี้ ขอความกรุณาติดต่อที่เจ้าหน้าที่ผ่าน [FaceBook Pages](https://www.facebook/adiwitcoth)

- โปรดตรวจสอบข้อมูล ไฟล์ ER Diagram ได้จาก resources/assets/ERDiagram/<project_name>.pdf

## การใช้งาน PHP Artisan จาก Docker
```
docker exec -it <project_name> php artisan migrate
```

## การใช้งาน PhpMyAdmin
ภายหลังจากที่ได้เปิดเซิร์ฟเวอร์จำลองขึ้นมาแล้ว Developer สามารถเข้าใช้งาน PHPMyAdmin ได้โดยเปิดผ่าน browser ที่ URL (http://localhost:8888) ข้อมูลเพิ่มเติมและวิธีใช้งาน Docker [คลิ๊ก](https://docs.docker.com/get-started)

## การวางไฟล์
บริษัทฯเชื่อว่าซอฟต์แวร์คุณภาพเริ่มต้นจากโค๊ดที่เขียนขึ้นตามฟอร์แม่ทมาตรฐานสากล บริษัทฯใช้ GitLab ในการทำ Automated Testing เบื้องต้นในการลดภาระของ Software Tester ของบริษัทฯ และเป็นการช่วย Developer ในการตรวจสอบผลลัพธ์ก่อนส่งมอบงานได้แบบ Real Time โดยเข้าไปที่ `https://<project_name>.durian.software`

### ไฟล์ Test
- กรุณาเก็บไฟล์ของคุณใว้ที่ `tests/Unit/BackOffice/<project_name>/` โดยแบ่งแยกตาม RESTful_action ดังนี้ :
    - <project_name>CreateTest.php
    - <project_name>DeleteTest.php
    - <project_name>DestroyTest.php
    - <project_name>ReadTest.php
    - <project_name>RestoreTest.php
    - <project_name>UpdateTest.php

และเพิ่มเติมอีก 2 TestCase คือ:
    - <project_name>SearchTest.php
    - <project_name>RouteTest.php

### ไฟล์ Migration
วิธีการตั้งชื่อไฟล์ ขอให้ตั้งชื่อตาม action ที่เกิดขึ้นโดยใช้ [snake_case](https://en.wikipedia.org/wiki/Snake_case) ตามคำแนะนำของ [Laravel](https://laravel.com/docs/5.5/migrations#generating-migrations) โดย Developer สามารถใช้คำสั่ง php artisan make:migration <database_action_name> -all ที่มาพร้อมกับ Laravel เพื่อช่วยในการสร้าง Migration นี้ได้ เช่น php artisan make:migration create_dim_examples_table หรือ php artisan make:migration add_companies_to_dim_examples_table เป็นต้น
- กรุณาเก็บไฟล์ของคุณใว้ที่ `databases/migrations/` โดยไม่ต้องใส่โฟลเดอร์ย่อยอะไรเพิ่มเติม
- โปรดตั้งชื่อ table ตามที่ระบุให้ใน ER Diagram
- ใช้ชื่อ table แบบพหุพจน์ (Plural) เช่น dim_companies แทนที่จะเป็น dim_company

#### ไฟล์ Model
- กรุณาเก็บไฟล์ของคุณใว้ที่ `app/` โดยใช้ [PascalCase](https://en.wikipedia.org/wiki/PascalCase) ไม่ต้องใส่โฟลเดอร์ย่อยอะไรเพิ่มเติม
- ตั้งชื่อ ​Model ตามชื่อ table ที่ระบุใน ER Diagram โดยตัดคำว่า dim หรือ fact ทิ้ง เช่น dim_users => User
- ใช้ชื่อ Model แบบเอกพจน์ (Singular) เช่น Company แทนที่จะเป็น Companies
- ในกรณีที่ Developer ได้รับงานในโมดูลที่มี Relationship (ForeignKey, 1-to-many หรือ many-to-many) ขอความกรุณา Developer สร้าง Model เปล่าๆขึ้นมาเพื่อรองรับ Relationship นี้ และเพิ่ม function ที่เกี่ยวข้อง เช่น BelongsTo, HasMany, HasOne, ManyToMany เป็นต้นให้กับทางบริษัทฯด้วย

#### ไฟล์ Seed
- กรุณาเก็บไฟล์ของคุณใว้ที่ `databases/seeds/BackOffice/<project_name>/` และขอความกรุณาใช้ Factory + Faker ในการสร้าง Seed โดยให้สร้างข้อทมูลตัวอย่าง อย่างน้อย 100 records

#### ไฟล์ Factory
- กรุณาเก็บไฟล์ของคุณใว้ที่ `databases/factories/<project_name>`

### ไฟล์ Controller
เพื่อให้ Developer ทำงานได้อย่างสะดวก สามารถปิดงานได้อย่างรวดเร็ว และย่นระยะเวลาการตรวจรับงานของทีมงานบริษัทฯ ขอความกรุณา Developer ใช้ [Resource Controller](https://laravel.com/docs/5.5/controllers#resource-controllers) โดยคำนึงถึงคอนเซ็ปต์ CRUD ในการเขียน Controller
- กรุณาเก็บไฟล์ของคุณใว้ที่ `app/Http/Controllers/BackOffice/` ในรูปแบบ [PascalCase](https://en.wikipedia.org/wiki/PascalCase) โดยไม่ต้องใส่โฟลเดอร์ย่อยอะไรเพิ่มเติม

ทีมงานของบริษัทฯเข้าใจดีว่า Resource Controller นั้นไม่ได้มี function ในส่วนของการ Restore และ ForceDelete ตามที่ระบุใน ER Diagram มาให้ จึงขอความกรุณา Developer เพิ่มเติมในส่วนของฟังก์ชั่น Restore ดังนี้:

```
/**
 * Restore the specified resource from Soft Deletion.
 *
 * @param  int  $id
 * @return \Illuminate\Http\Response
 */
public function restore($id)
{
    $model->relationship()->restore();
    return redirect()->route('<project_name>.index')->with('success', 'Restore success');
}
```

และเพิ่ม Route ดังนี้:
```
Route::get('<project_name>/{id}/restore', ['as' => '<project_name>.restore', 'uses' => 'BackOffice\<project_name>Controller@restore']);
```

สำหรับการทำ ForceDelete นั้นขอให้ ​Developer ใช้ฟังก์ชั่นเดียวกับการทำ softDelete กล่่าวคือให้ใช้ฟังก์ชั่น destroy ที่มาให้กับ Resource Controller อยู่แล้วดังนี้:

```
$model = Model::withTrashed()->where('id', 1)->first();
if ($model->trashed()) {
    return $model->relationship()->forceDelete();
}
return $model->relationship()->delete();
```

#### Nested Resources Controller
ในกรณีที่ Developer ได้รับโมดูลที่เชื่อมต่อกัน เช่น Post > Comments ขอความกรุณา Developer ใช้ [Nested Resource](https://laravel.com/docs/5.1/controllers#restful-nested-resources) เพื่อให้ Developer ทำงานได้อย่างสะดวก สามารถปิดงานได้อย่างรวดเร็ว และย่นระยะเวลาการตรวจรับงานของทีมงานบริษัทฯ

### ไฟล์ View
เนื่องจากบริษัทฯ แบ่งการทำงานระหว่าง BackEnd Developer ออกจาก FrontEnd Web Developer บริษัทฯจึงขอความกรุณา BackEnd Developer เขียน Code ในส่วนของ HTML, CSS, และ​ JavaScript ให้น้อยที่สุด โดยให้คำนึงว่าจุดประสงค์ของการเขียน​ View ในครั้งนี้คือแค่ให้เพียงพอที่ FrontEnd Developer (ผู้ซึ่งไม่ถนัด Logical Coding) สามารถหยิบ code ของคุณไปวางในที่ๆเหมาะสมได้อย่างง่ายดาย

```
<form action="{{ route('example.store') }}" method="POST">
    {!! csrf_field() !!}

    <!-- EXAMPLE SELECT -->
    <select name="field_1[]" id="field_1">
        <option value="" disabled="disabled">-- Field 1 --</option>
        <option value="{{ old('field_1')}}" @if( old('field_1')) selected="selected" @endif >Value 1</option>
        <option value="{{ old('field_1')}}" @if( old('field_1')) selected="selected" @endif >Value 2</option>
    </select>
    
    <!-- EXAMPLE INPUT -->
    <input type="text" name="field_2" id="field_2" placeholder="field_2" value="{{ old('field_2') }}" required>
    
    <!-- EXAMPLE TEXTAREA -->
    <textarea name="field_3" id="field_3" placeholder="field_3">{{ old('field_3') }}</textarea>

    <!-- EXAMPLE RADIO -->
    <input type="radio" name="field_4" value="1" id="field_4" @if( old('field_4')) checked @endif> Active
    <input type="radio" name="field_4" value="0" id="field_4" @if(! old('field_4')) checked @endif> Inactive

    <!-- EXAMPLE CHECKBOX -->
    <input type="checkbox" name="field_5[]" value="1" id="field_5" @if( old('field_5')) checked @endif> Active
    <input type="checkbox" name="field_5[]" value="0" id="field_5" @if(! old('field_5')) checked @endif> Inactive

    <button type="submit">Submit</button>
</form>

<!-- ERROR MESSAGES -->
<div>Error Message</div> 
```

- กรุณาเก็บไฟล์ของคุณใว้ที่ `resources/views/BackOffice/<project_name>/<RESTful_action>.blade.php`


### ไฟล์ Request (Validation และ ​Message)
- กรุณาเก็บไฟล์ของคุณใว้ที่ `app/Http/Requests/BackOffice/<project_name>/`

## Scope งาน :
- UnitTest​
- Migration
- Model
- Seed
- Factory
- Controller
- Request (Validation และ ​Message)