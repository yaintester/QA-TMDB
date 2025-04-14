## Technical Test QA - Nisrina Athiyya Zain
----------------
## Task yang dikerjakan
Membuat skenario pengujian  dalam bentuk test case dan bug report:
1. Ubah bahasa menjadi bahasa indonesia
2. User hanya bisa melakukan ”mark as favorite” ketika dia sudah login
3. Ketika user melakukan “mark as favorite” dari suatu film, maka film tersebut akan tersimpan di bagian favorite movies di profil pengguna
4. User bisa memfavorite lebih dari 1 movie dan validasi hasilnya
5. User bisa meremove movie dari daftar favorite movies di favorite list
6. User bisa mengurutkan / ordering daftar favorite movies dia
Ubah kembali ke bahasa Inggris lalu lakukan regresi test kembali

### Berikut adalah link test case dari pengujian diatas:
https://docs.google.com/spreadsheets/d/1gsR91N2kBrsL1YYUwuXSfCXGyNvVFPEJfgIvnVNsy2U/edit?usp=sharing

### Berikut adalah bug report dari pengujian diatas: 
https://docs.google.com/document/d/1_AeekFK1NrJlB10DOOtcGZ8jZYFq27XL/edit?usp=sharing&ouid=103718986905701257299&rtpof=true&sd=true

### Untuk Example dari step to reproduce dan screnshoot/video mengenai bug dapat dilihat pada folder exmaple of step to reproduce dan folder bug

### Berikut adalah scenario pengujian dalam format gherkin:
```
Feature: Change Language Feature on TMDb
  As a user, I want to change the website language and verify the changes.

  Scenario: Change Language to Indonesian
    Given the user is on the page "https://www.themoviedb.org/"
    When the user clicks on the language icon
    And the user sets the "Default Language" to Indonesian (ID)
    And the user sets the "Fallback Language" to Arabic (AR)
    And the user clicks the "Reload Page" button
    Then the page should display in Indonesian if available
    And if Indonesian is unavailable, the page should display in Arabic as fallback.

  Scenario: Save Language Settings and Verify Fallback
    Given the user is on the page "https://www.themoviedb.org/"
    When the user clicks on the language icon
    And the user sets the "Default Language" to Indonesian (ID)
    And the user sets the "Fallback Language" to Arabic (AR)
    And the user clicks the "Reload Page" button
    Then the page should display in Indonesian with Arabic as fallback if needed.

  Scenario: Do Not Save Language Settings
    Given the user is on the page "https://www.themoviedb.org/"
    When the user clicks on the language icon
    And the user sets the "Default Language" to Indonesian (ID)
    And the user sets the "Fallback Language" to Arabic (AR)
    And the user refreshes the page
    Then the language settings should revert to the previous state.

Feature: Mark as Favorite Feature on TMDb
  As a user, I want to mark and manage my favorite movies on TMDb.

  Scenario: Mark a Movie as Favorite
    Given the user is logged in and on the movie page
    When the user selects a movie with Movie ID "1032823"
    And the user clicks the "Favorite" button
    Then the movie should be visible in the user's favorite list under "Most Favorite".

  Scenario: Mark a Movie as Favorite Without Logging In
    Given the user is not logged in
    When the user selects a movie with Movie ID "1032823"
    And the user clicks the "Favorite" button
    Then the user should be prompted to log in before marking the movie as favorite.

  Scenario: Mark Multiple Movies as Favorites
    Given the user is logged in and on the movie pages
    When the user selects movies with IDs "1032823", "1022789", "533535"
    And the user clicks the "Favorite" button for each movie
    Then all selected movies should appear in the user's favorite list.

  Scenario: Sort Favorite Movies
    Given the user is logged in and has movies in the favorite list
    When the user sorts the movies by "Highest User Score"
    Then the movies should be displayed sorted as per the selected preference.

  Scenario: Sort Favorite Movies Without Items in the List
    Given the user is logged in and the favorite list is empty
    When the user tries to sort the favorite list
    Then the user should see a message indicating that the list is empty.

  Scenario: Remove Movies from Favorite List
    Given the user is logged in and has movies in the favorite list
    When the user selects a movie with Movie ID "1032823"
    And the user clicks the "Remove" button
    Then the movie should no longer exist in the favorite list.

  Scenario: Remove a Movie Not in Favorite List
    Given the user is logged in and the movie with Movie ID "533535" is not in the favorite list
    When the user tries to remove the movie from the favorite list
    Then the user should see a message indicating that the movie is not in the list.

  Scenario: Remove a Movie from Movie Page
    Given the user is logged in and has movies in the favorite list
    When the user visits the movie page of a movie with Movie ID "1032823"
    And the user clicks the "Favorite" icon to unmark the movie
    Then the movie should no longer exist in the user's favorite list.
```
## Feedback/Saran untuk UI UX
- Pengguna tidak bisa menghapus favorit film dari list film foavorite (tombol remove dan tombol love tidak bekerja) --> mengakibarkan user harus mengeklik satu satu film kemudian meremove love satu persatu.Mengakibatkan pengalaman pengguna yang buruk, tidak effisien, memakan banyak waktu user.

- Horizontal scroll bar pada menu utama warna tidak begitu jelas, pengguna susah menemukan, buat agar lebih terlihat dan tetap intuitif

- Efek fade sebaiknya dihilangkan saja atau diperbaiki agar lebih intuitif (tetap memperhatikan simetrisitas)

- Logo pada bagian bawah baiknya diperkecil jadi tata letaknya lebih rapi 

- Dalam fitur ubah bahasa perbaiki: "Default Language" dan "Fallback Language" mungkin membingungkan bagi pengguna non-teknis. Mereka mungkin tidak memahami apa yang dimaksud dengan fallback language atau kapan ini diterapkan. Selain itu ebih baik menggunakan istilah save dari pada reload page
