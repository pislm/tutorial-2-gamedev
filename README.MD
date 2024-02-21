# Tutorial 2 GameDev
Hafizh Salam - 1906399171

### Latihan: Playtest
- Apa saja pesan log yang dicetak pada panel Output?  
Pesan log yang dicetak pada panel Output yaitu
    ```
    --- Debugging process started ---
    Godot Engine v3.5.3.stable.official.6c814135b - https://godotengine.org
    OpenGL ES 3.0 Renderer: Apple M1 Pro
    Async. shader compilation: OFF
    
    Registered camera FaceTime HD Camera with id 1 position 0 at index 0
    Registered camera Apissss Camera with id 2 position 0 at index 1
    Platform initialized
    Reached objective!
    Reached objective!
    --- Debugging process stopped ---
    ```
- Coba gerakkan landasan ke batas area bawah, lalu gerakkan kembali ke atas hingga hampir menyentuh batas atas. Apa saja pesan log yang dicetak pada panel Output?  
Pesan log yang dicetak pada panel Output yaitu
    ```
    Reached objective!
    Reached objective!
    ```
- Buka scene MainLevel dengan tampilan workspace 2D. Apakah lokasi scene ObjectiveArea memiliki kaitan dengan pesan log yang dicetak pada panel Output pada percobaan sebelumnya?  
Berdasarkan percobaan permainan, pesan log `Reached objective` akan muncul ketika pesawat berada pada bagian atas layar. Berdasarkan scene `MainLevel`, dapat dilihat bahwa `ObjectiveArea` mempunyai node `CollisionShape`. lalu dapat dilihat pada script `ObjectiveArea.gd`
    ```gd
    extends Area2D

    func _on_ObjectiveArea_body_entered(body: RigidBody2D):
        if (body.name == "BlueShip"):
            print("Reached objective!")
    ```
    Berdasarkan dokumentasi Godot, `body_entered ( Node2D body )` akan terpanggil sebuah `body` memasuki area bersangkutan, disini yaitu `ObjectiveArea`. Setelah dicek bahwa body tersebut merupakan `BlueShip`, maka akan dilakukan `print("Reached objective!")`. Dengan begitu dapat disimpulkan bahwa `Reached objective!` akan muncul di Output setiap `BlueShip` memasuki `ObjectiveArea`.

### Latihan: Memanipulasi Node dan Scene
- Scene BlueShip dan StonePlatform sama-sama memiliki sebuah child node bertipe Sprite. Apa fungsi dari node bertipe Sprite?  
Setelah mencoba untuk menyembunyikan sprite dari node, saya mendapatkan kesimpulan bahwa sprite merupakan tampilan/aset gambar dari node tersebut.
- Root node dari scene BlueShip dan StonePlatform menggunakan tipe yang berbeda. BlueShip menggunakan tipe RigidBody2D, sedangkan StonePlatform menggunakan tipe StaticBody2D. Apa perbedaan dari masing-masing tipe node?  
`RigidBody2D` merupakan sebuah body yang dapat merespon terhadap gaya, tabrakan, dorongan dan gravitasi. Sedangkan `StaticBody2D` biasanya digunakan untuk objek yang tidak bergerak terhadap gaya/dorongan fisika, namun dapat bertabrakan dengan objek lain seperti dinding dan tanah.
- Ubah nilai atribut Mass dan Weight pada tipe RigidBody2D secara bebas di scene BlueShip, lalu coba jalankan scene MainLevel. Apa yang terjadi?  
Setelah saya mencoba mengubah-ubah Mass dan Weight, tidak terjadi perubahan pada permainan. Menurut saya, ini dikarenakan karena kecepatan jatuhnya sebuah objek oleh gravitasi tidak dipengaruhi oleh massa/berat nya, dimana rumus kecepatan pada detik ke t yaitu $v = gt$, sehingga pergerakan objek akan tetap sama tidak peduli berat/massa nya.
- Ubah nilai atribut Disabled pada tipe CollisionShape2D di scene StonePlatform, lalu coba jalankan scene MainLevel. Apa yang terjadi?  
Setelah nilai Disabled diaktifkan, maka pesawat akan menembus objek `StonePlatform`. ini dikarenakan status *collision* menjadi *disabled* sehingga objek lain tidak menabrak dan langsung menembus objek tersebut.
- Pada scene MainLevel, coba manipulasi atribut Position, Rotation, dan Scale milik node BlueShip secara bebas. Apa yang terjadi pada visualisasi BlueShip di Viewport?  
`Position` menentukan posisi BlueShip pada axis x dan y, `Rotation` memutar arah Blueship, sedangkan `Scale` digunakan untuk mengatur ukuran, memperbesar/memperkecil BlueShip.
- Pada scene MainLevel, perhatikan nilai atribut Position node PlatformBlue, StonePlatform, dan StonePlatform2. Mengapa nilai Position node StonePlatform dan StonePlatform2 tidak sesuai dengan posisinya di dalam scene (menurut Inspector) namun visualisasinya berada di posisi yang tepat?  
Hal ini dikarenakan `StonePlatform` dan `StonePlatform2` merupakan child dari `PlatformBlue`, sehingga nilai posisi nya merupakan nilai relatif terhadap `PlatformBlue`.

### Latihan Mandiri: Membuat Level Baru

Pada latihan mandiri ini, saya memodifikasi PlatformBlue agar memiliki dinding di sebelah kiri, serta membuat `ObjectiveArea` pada bagian kanan atas. dan membuat platformblue bisa bergerak ke kanan dan kiri.