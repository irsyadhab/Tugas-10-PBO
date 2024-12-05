# Tugas 10 PBO
Nama  : Muhammad Irsyad Habibi
NRP  : 5025221150
Kelas  : PBO A

# Class SalesItem

```
import java.util.ArrayList;
import java.util.List;

public class SalesItem {
  private String itemName;
  private double price;
  private List<Comment> comments;

  public SalesItem(String itemName, double price) {
    this.itemName = itemName;
    this.price = price;
    this.comments = new ArrayList<>();
  }

  public void addComment(String author, String text, int rating) {
    if (rating < 1 || rating > 5) {
      throw new IllegalArgumentException("Rating harus antara 1 dan 5.");
    }
    comments.add(new Comment(author, text, rating));
  }

  public int getNumberOfComments() {
    return comments.size();
  }

  public List<Comment> getComments() {
    return new ArrayList<>(comments);
  }

  public String getItemName() {
    return itemName;
  }

  public double getPrice() {
    return price;
  }
}
```
Kelas ini merepresentasikan sebuah item yang dijual, dengan atribut utama:

- `itemName`: Nama dari item.
- `price`: Harga item.
- `comments`: Daftar komentar terkait item, menggunakan objek Comment.

Fungsi utama:

- Konstruktor:
  - Menginisialisasi nama item, harga, dan membuat list kosong untuk komentar.
- Metode `addComment(String author, String text, int rating)`:
  - Menambahkan komentar baru pada item.
  - Memastikan bahwa rating berada dalam rentang 1 hingga 5, jika tidak, akan memunculkan pengecualian (IllegalArgumentException).
- Metode `getNumberOfComments()`:
  - Mengembalikan jumlah komentar yang telah ditambahkan pada item.
- Metode `getComments()`:
  Mengembalikan salinan daftar komentar, sehingga tidak bisa dimodifikasi langsung.
- Getter:
  - getItemName() untuk mendapatkan nama item.
  - getPrice() untuk mendapatkan harga item.

Summary:
Kelas ini bertugas untuk menyimpan informasi item yang dijual beserta daftar komentar dan memfasilitasi penambahan komentar.


# Class Comment

```
public class Comment {
  private String author;
  private String text;
  private int rating;

  public Comment(String author, String text, int rating) {
    this.author = author;
    this.text = text;
    this.rating = rating;
  }

  public String getAuthor() {
    return author;
  }

  public String getText() {
    return text;
  }

  public int getRating() {
    return rating;
  }
}
```
Kelas ini merepresentasikan sebuah komentar terkait dengan item, dengan atribut:

- `author`: Nama orang yang memberikan komentar.
- `text`: Isi komentar.
- `rating`: Penilaian dalam bentuk angka (1-5).

Fungsi utama:
- Konstruktor:
  Menginisialisasi nama penulis, teks komentar, dan rating.
- Getter:
  `getAuthor()` untuk mendapatkan nama penulis.
  `getText()` untuk mendapatkan isi komentar.
  `getRating()` untuk mendapatkan nilai rating.
  
Summary:
Kelas ini bertugas untuk menyimpan informasi satu komentar yang dibuat oleh pengguna.4

# Class SalesItemTest
```
import org.junit.Test;
import static org.junit.Assert.*;
import java.util.List;

public class SalesItemTest {

  @Test
  public void testAddComment() {
    SalesItem item = new SalesItem("Tablet", 300.0);
    item.addComment("David Smith", "Amazing quality!", 5);
    assertEquals(1, item.getNumberOfComments());
  }

  @Test
  public void testAddInvalidComment() {
    SalesItem item = new SalesItem("Tablet", 300.0);
    assertThrows(IllegalArgumentException.class, () -> item.addComment("Emily Brown", "Poor design", 0));
  }

  @Test
  public void testGetComments() {
    SalesItem item = new SalesItem("Headphones", 120.0);
    item.addComment("Sarah Johnson", "Comfortable and great sound", 4);
    item.addComment("Michael Lee", "Average experience", 3);

    List<Comment> comments = item.getComments();

    assertEquals(2, comments.size());
    assertEquals("Sarah Johnson", comments.get(0).getAuthor());
    assertEquals("Comfortable and great sound", comments.get(0).getText());
  }
}
```

Kelas ini adalah unit test menggunakan framework JUnit untuk memastikan bahwa kelas SalesItem bekerja sesuai spesifikasi.

Fungsi utama:
- testAddComment():
  - Menguji apakah komentar berhasil ditambahkan pada item.
  - Menggunakan assertEquals untuk memverifikasi jumlah komentar setelah penambahan.
- testAddInvalidComment():
  - Menguji apakah penambahan komentar dengan rating tidak valid (kurang dari 1 atau lebih dari 5) memunculkan pengecualian (IllegalArgumentException).
  - Menggunakan assertThrows untuk memverifikasi bahwa pengecualian dilempar.
- testGetComments():
  - Menguji apakah daftar komentar yang dikembalikan sesuai dengan komentar yang telah ditambahkan.
  - Memverifikasi isi daftar menggunakan assertEquals.
  - 
Summary:
Kelas ini digunakan untuk memastikan bahwa:
- Penambahan komentar berfungsi dengan benar.
- Penanganan input invalid berjalan sesuai spesifikasi.
- Daftar komentar dapat diambil dan isinya sesuai.
