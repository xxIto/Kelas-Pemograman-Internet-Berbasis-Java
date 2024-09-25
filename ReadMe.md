# Yang Harus Di Install
- JDK
- Apache Maven
- Tomcat / XAMPP
- Ekstensi  ```Java Extension Pack``` di VScode

---
# Langkah - Langkah
## Buat Proyek Maven
- Buka VScode, tekan ```Ctrl + Shift + P```, dan ketik ```Maven: New Project```
- Pilih template project ```maven-archetype-webapp```
- Pilih versi Maven
- Masukkan ```groupId``` (misalnya : ```com.example```)
- Masukkan ```artifactId``` (misalnya : ```nama-project```)
- Pilih lokasi penyimpan proyek

---
## Konfigurasi ```pom.xml```
- Buka file ```pom.xml``` dan tambahkan dependensi untuk ```Servlet API```
```
<dependencies>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

---
## Tambah File JSP dan Servlet
- JSP : Tambahkan file .jsp di folder ```src/main/webapp```. Biasanya sudah ada saat awal install. Jika belum buat file ```index.jsp``` dengan isi seperti ini :
```
<html>
<body>
    <h2>Welcome to My JSP Page</h2>
</body>
</html>
```
  
- Servlet : Buat kelas Servlet di folder ```src/main/java``` seperti ini :
```
package com.example;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        RequestDispatcher dispatcher = request.getRequestDispatcher("/index.jsp");
        dispatcher.forward(request, response);
    }
}
```

---
## Konfigurasi ```web.xml```
- Tambahkan pengaturan Servlet di file ```web.xml``` di folder ```WEB-INF/``` jika kalian ingin menggunakan konfigurasi XML

## Build Project
- Di terminal VScode, jalankan perintah berikut :
```
mvn clean package
```

## Deploy ke Tomcat
- Setelah build selesai, file ```.war``` akan dibuat di folder ```target/```
- Copy file ```.war``` tersebut ke folder ```webapps``` di direktori Tomcap
- Jalan Tomcat dari XAMPP Control Panel dan buka ```http://localhost:8080/nama-project``` untuk melihat aplikasi kalian