# Analisis Konsep MVC pada Direktori Laravel 11

Laravel 11 menggunakan arsitektur **MVC (Model–View–Controller)** sebagai pola utama untuk memisahkan logika aplikasi. Struktur direktori Laravel membantu pengembang menjaga kode tetap bersih, rapi, modular, dan mudah dipelihara.

---

## 1. **Model (app/Models)**
Model mewakili **lapisan data** dan berfungsi sebagai penghubung antara aplikasi dan database melalui **Eloquent ORM**.

### **Lokasi Direktori**
```
app/
 └── Models/
```

### **Peran Model**
- Berinteraksi dengan database (select, insert, update, delete).
- Mengatur relasi antar tabel (hasMany, belongsTo, dll).
- Menyediakan fitur accessor, mutator, casting, dan query scope.
- Menangani logika yang berhubungan dengan data.

### **Contoh Model**
```php
class Product extends Model
{
    protected $fillable = ['name', 'price'];
}
```

---

## 2. **View (resources/views)**
View merupakan **lapisan presentasi** yang ditampilkan kepada pengguna menggunakan Blade Template Engine.

### **Lokasi Direktori**
```
resources/
 └── views/
```

### **Peran View**
- Menampilkan UI berbasis Blade.
- Merender data yang dikirim dari Controller.
- Menggunakan directive Blade seperti `@if`, `@foreach`, `@include`, dan komponen Blade.

### **Contoh View (Blade)**
```blade
<h1>{{ $product->name }}</h1>
<p>Harga: {{ $product->price }}</p>
```

---

## 3. **Controller (app/Http/Controllers)**
Controller adalah **lapisan logika aplikasi** yang mengatur alur request dan response, serta menghubungkan Model dan View.

### **Lokasi Direktori**
```
app/
 └── Http/
     └── Controllers/
```

### **Peran Controller**
- Mengambil dan memproses request dari user.
- Mengambil data dari Model.
- Mengirim data ke View.
- Menjalankan validasi input.
- Mengatur proses CRUD dan sebagian logic bisnis.

### **Contoh Controller**
```php
class ProductController extends Controller
{
    public function show($id)
    {
        $product = Product::findOrFail($id);
        return view('product.show', compact('product'));
    }
}
```

---

# Alur Kerja MVC di Laravel 11
1. User mengirim request ke aplikasi.
2. Route menentukan controller mana yang dijalankan.
3. Controller memanggil Model untuk mengambil atau memproses data.
4. Controller mengirim data tersebut ke View.
5. View dirender menjadi HTML.
6. HTML dikembalikan ke user sebagai response.

---

# Direktori Pendukung dalam Arsitektur MVC
Selain folder inti MVC, Laravel memiliki beberapa direktori penting lain:

| Direktori | Fungsi |
|----------|--------|
| `routes/` | Menentukan endpoint dan menghubungkannya dengan controller. |
| `database/migrations/` | Mengatur struktur tabel database. |
| `database/seeders/` | Mengisi data awal. |
| `app/Http/Middleware/` | Menyaring request (auth, throttle, dll). |
| `resources/js` & `resources/css` | Asset frontend. |

---

# Kesimpulan
- **Model** mengatur data dan berinteraksi dengan database.
- **View** menampilkan UI untuk pengguna.
- **Controller** mengatur alur aplikasi dan menghubungkan Model ↔ View.

Struktur direktori Laravel 11 memudahkan implementasi arsitektur MVC secara bersih dan scalable.

