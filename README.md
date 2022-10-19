# ComparisonReport
Generate Otomatis Report Perbandingan Data Sales (Daily)

Secara garis besar tools ini akan mengenerate report daily yang berisi perbandingan data sales antar database. 
</br>
Tools ini dibuat dengan menggunakan **Pentaho Data Integration**.

Berikut interface dari tools yang saya buat:
![image](https://user-images.githubusercontent.com/32997439/196588041-5202d6b0-534a-4f8e-af0f-929ceedf2661.png)

Tahapan yang dilakukan adalah 
1. Tools akan mengambil tanggal yang akan diambil data salesnya dari database Profit.
![image](https://user-images.githubusercontent.com/32997439/196592362-21abd790-fe5b-4343-afb6-660fb43b4f97.png)

2. Dilakukan proses looping insert data sesuai dengan banyaknya tanggal yang akan diambil datanya. 
![image](https://user-images.githubusercontent.com/32997439/196592593-e90e7a23-45db-466c-b271-a11f570325d9.png)
Di dalam job **JOB_INSERT_GRAB_POS_PROFIT** berisi proses delete data yang sudah ada agar tidak terjadi duplikasi data.
</br>Kemudian sumber data yang diambil dari JSON dimasukkan ke dalam tabel yang ada di database profit dan database radar.

3. Tools akan mengambil data sales dari tim GRAB berupa file CSV yang sudah diletakkan di dalam FTP.
![image](https://user-images.githubusercontent.com/32997439/196592638-ed1df5d9-9461-47c0-861b-c0d42bee903c.png)

4. File tersebut akan disimpan dalam folder lokal, jika terdapat file maka tools akan mengambil data tanggal yang ada pada nama file.
![image](https://user-images.githubusercontent.com/32997439/196592681-96d5b064-dd2d-48cc-8fb7-33e74b577edc.png)

5. Tools akan melakukan proses looping untuk melakukan insert data sesuai dengan jumlah file. 
![image](https://user-images.githubusercontent.com/32997439/196592735-460ab226-105f-4e6e-bfd7-931875d3b123.png)
Di dalam job **JOB_INSERT_GRAB_FILE** berisi proses delete data yang sudah ada agar tidak terjadi duplikasi data.
</br>Kemudian sumber data yang diambil dari file CSV dimasukkan ke dalam tabel yang ada di database radar.
</br>Setelah semua data sukses diinsert, tools akan mengenerate report yang berisi komparasi data yang bersumber dari JSON dan CSV yang sudah ada di database radar.
</br>

6. Jika report sudah terbentuk, report akan di zip dan dimasukkan ke dalam FTP.
![image](https://user-images.githubusercontent.com/32997439/196593270-92c0d2d0-838c-4677-a794-9b40080abfee.png)

7. Report komparasi tersebut akan ditampilkan di website **Report Portal** dan dapat diunduh oleh user yang bersangkutan.
8. Selain itu, perbandingan data total sales setiap harinya akan ditampilkan dalam website **Radar**.
