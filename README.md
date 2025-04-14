# TMDb Feature Testing – QA Portfolio

## 📋 Task Overview
This project demonstrates a QA testing task focused on validating key functionalities of [TMDb (The Movie Database)](https://www.themoviedb.org/), specifically the **"Mark as Favorite"** and **"Change Language"** features. It includes detailed test cases, bug reports, regression testing, and UI/UX feedback.

---

## ✅ Scope of Testing

### 1. **Mark as Favorite Functionality**
- User can only "mark as favorite" **after logging in**
- Favorited movies are saved in the user's **Favorite Movies** list
- User can favorite **multiple movies** and validate all entries
- User can **remove movies** from the Favorite list
- User can **sort/order** movies in the Favorite list

### 2. **Change Language Functionality**
- Change website language to **Indonesian**
- Apply **Fallback Language** to **Arabic** if content is unavailable in Indonesian
- Perform **regression test** after language change to ensure consistency

---

## 🧪 Test Documentation

- 📄 [Test Case Sheet](https://docs.google.com/spreadsheets/d/1gsR91N2kBrsL1YYUwuXSfCXGyNvVFPEJfgIvnVNsy2U/edit?usp=sharing)  
- 🐞 [Bug Report Document](https://docs.google.com/document/d/1_AeekFK1NrJlB10DOOtcGZ8jZYFq27XL/edit?usp=sharing&ouid=103718986905701257299&rtpof=true&sd=true)  

---

## 🔍 Gherkin-Based Test Scenarios

### Feature: Change Language on TMDb
```gherkin
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
- Inability to bulk-remove favorite movies results in a poor user experience
- Scroll bar on the main menu is not clearly visible
- Fade effects are unintuitive and need improvement
- Footer logo size and layout could be better optimized
- "Default Language" and "Fallback Language" terms may confuse non-technical users – suggested using more intuitive labels like "Save Language Settings"
