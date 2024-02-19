<h1 align="center">
  <a href="https://github.com/SBNZ-SmFoYcSNaQ">
    Bookstore-Bank 
  </a>
</h1>

<div align="center">
  <a href="#about"><strong>Explore the screenshots »</strong></a>
  <br />
  <br />
</div>

<details open="open">
<summary id="table-of-contents">Table of Contents</summary>

- [About](#about)
  - [Rules](#rules)
  - [Built With](#built-with)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Authors](#authors)

</details>

---

## About
This project was developed as part of the Knowledge Based Systems course at the Faculty of Technical Sciences by a team of 4 people. The primary objective of this project was to familiarize ourselves with rule-based systems. 

To accomplish this, we created two systems: an online bookstore and a bank. These two services were designed to cooperate with each other, allowing bookstore users to purchase books using a payment card. The system's modular structure is illustrated below.

<div align="center">
  
  ![Structure](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/0831bd86d758bb1d1219f24e630526ec4ae75926/profile/images/structure.svg)
</div>


<div style="display: flex; justify-content: space-around;">
<div>
<details>
<summary><b>Bookstore functionalities:</b></summary>

- Registration
- Login
- Books overview
- Books rating
- Books recommendation for unauthenticated user
- Books recommendation for logged in user
- Order creation and discount calculation
- Payment of the order by cash on delivery
- Payment of the order by payment card


</details>
</div>
<div>
<details>
<summary><b>Bank functionalities:</b></summary>

- Registration
- Login
- Multiple accounts creation
- Credit application processing
- Transaction processing
- Payment card fraud detection

</details>
</div>
</div>
<br>

<details>
<summary>Screenshots</summary>
<br>
<div align="center">
  <h2>Bookstore</h2>
</div>

| Home Page | Login Page |
| :-------: | :--------: |
| ![Home Page](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bookstore/home.png) | ![Login Page](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bookstore/login.png) |

| Home Page For Logged-In Users | Books |
| :---------------------------: | :---: |
| ![Home Page For Logged-In Users](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bookstore/logged_in_home.png) | ![Books](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bookstore/books.png) |

| Cart | Payment |
| :--: | :-----: |
| ![Cart](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bookstore/cart.png) | ![Payment](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bookstore/payment.png) |

<div align="center">
  <h2>Bank</h2>
</div>

| Registration Page | Login Page |
| :-------: | :--------: |
| ![Registration Page](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bank/registration.png) | ![Login page](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bank/login.png) |

| Bank Accounts | Suspicious Transactions |
| :-----------: | :---------------------: |
| ![Bank Accounts](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bank/bank_accounts.png) | ![Suspicious Transactions](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bank/suspicious_transactions.png) |

| Credit Application | System Response |
| :----------------: | :-------------: |
| ![Credit Application](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bank/credit_application.png) | ![System Response](https://raw.githubusercontent.com/SBNZ-SmFoYcSNaQ/.github/main/profile/images/bank/system_response.png) |

</details>

### Rules

- Bookstore
  - Items
    - Apply a 10% discount for items with a quantity of 2 or more
    - Apply a 5% discount for items with a total price exceeding 3000 RSD
    - Apply a 7% discount for items categorized as Educational content if their total price exceeds 2000 RSD
  - Orders
    - Apply a 10% discount for orders containing 3 or more items
    - Apply a 15% discount for orders containing 5 or more items
  - Books recommendations:
    - See detailed rules [here](#bookstore-rules)
- Bank
  - Issuance of credits to clients
    - Credits should have a minimum and maximum repayment period
    - The client must have a stable income during the credit repayment period
    - The income should be sufficient to cover the credit repayment
    - Existing credit obligations should be considered, including ongoing repayments of other credits
    - Elderly clients fall into the higher-risk category for long-term credits
    - Customers with a history of regular credit repayments should have an advantage
  - Card payment fraud detection 
    - Possible fraud indicators include:
      - Multiple temporally close transactions at remote locations
      - A high volume of small transactions within a short timeframe
      - Transactions originating from unfamiliar locations for the user
      - Large money transfers during unusual hours, such as at night
      - Transactions significantly exceeding the user's typical spending patterns

<div id="bookstore-rules"></div>
<details>
<summary><b>Bookstore Recommendations Rules</b></summary>

Books recommendations to unauthenticated users
  - A book is considered new if it was added to the bookstore's offer within the previous month
  - A book is considered new if it was published within the previous six months
  - A book is popular if it has 20 or more ratings
  - A book is popular if it is new and has 10 or more ratings
  - A book is rated well if it has an average rating of 4 or higher
  - A book is rated poorly if it has an average rating of 2.5 or less
  - A book is rated neutral if it has an average rating between 2.5 and 4 or no rating yet
  - If the book is popular and rated good or neutral, it should be recommended
  - If the book is new, it should be recommended
  - If the number of books to be recommended is greater than 10, those that have not been rated should be excluded
  - If the number of books to recommend exceeds 10 and after excluding the poorly rated ones, 10 titles should be randomly selected

Books recommendation for authenticated users
  - If the user is new (has rated fewer than 10 books), they will be prompted to choose their favorite genres during account creation. If they do not make a selection, recommended books to them in the same way as to an unauthenticated user
  - If the user makes a selection, recommend the top 10 highest-rated books by the most popular authors in the chosen genres. Popularity is determined by the total number of ratings received for the author's books. An author is associated with a genre if at least 30% of the books they have written belong to that genre
  ---
  - If the user is not new, a book can be recommended based on the preferences of similar users. User similarity is determined using the <a href="#pearson">Pearson correlation coefficient</a>. Two users are considered similar if the coefficient value is greater than or equal to 0.5. A user is considered to have liked a book if they rated it 4 or 5
  - A book can be recommended if it is similar to books the user has liked. Two books are considered similar if at least 70% of users who rated both books gave the same rating or a rating that differs by one.
  - A book can be recommended if it matches the user's preferences. It is considered that the user is interested in an author if they have bought at least 3 of the author's books in the previous 6 months. Similarly, it is considered that the user is interested in a genre if at least 30% of the books they bought in the previous 6 months belong to that genre
  - For each criterion that a book fulfills for recommendation, it receives one point. The final recommendation should consist of the top 20 highest-ranked books. In case there are more than 20 books with the same number of points, priority is given to new books.
</details>

<div id="pearson" align="center"> 
<details open>
<summary><b>Pearson Correlation Coefficient:</b></summary>
  <img src="profile/images/pearson.svg" title="Pearson Correlation Coefficient" width="55%">
</details>
</div>

### Built With

- [Java](https://www.java.com/)
- [Spring Boot](https://spring.io/)
- [Drools](https://www.drools.org/)
- [PostgreSQL](https://www.postgresql.org/)
- [React](https://react.dev/)
<div align="right">[ <a href="#table-of-contents">↑ Back to top ↑</a> ]</div>

## Getting Started

### Prerequisites

- **Java development kit (JDK)**: This is the core component that is required to develop, compile, and run Java applications. You can download the latest version of JDK from the [Java website](http://java.com)
- **PostgreSQL**: A robust open-source relational database system, that is a crucial requirement for this project. It serves as the primary database for storing and managing data. You can download it [here](https://www.postgresql.org/download/)
- **Node.js**: Node.js is essential for starting React projects. If you haven't installed Node.js, you can find installation instructions [here](https://nodejs.org)
- **Maven**: Maven is a build automation tool for Java projects. It manages dependencies, compiles code, runs tests, and packages applications. You can download it from the [Apache Maven website](https://maven.apache.org/download.cgi)

### Installation

For Maven installation, refer to the official Maven installation [guide](https://maven.apache.org/install.html).

Clone all pinned repositories from SBNZ-SmFoYcSNaQ organization using `git clone`.
```
git clone https://github.com/SBNZ-SmFoYcSNaQ/Bank
git clone https://github.com/SBNZ-SmFoYcSNaQ/bookstore-backend
git clone https://github.com/SBNZ-SmFoYcSNaQ/bookstore-frontend
```

**Database configuration**:
- Make sure you have PostgreSQL installed on your system
- Configure the database connection settings in the application.properties file. By default, the application uses the following credentials:
  - For bank application:
    ```
    spring.datasource.url = jdbc:postgresql://localhost:5432/bank
    spring.datasource.username = postgres
    spring.datasource.password = password
    ```
  - For bookstore application:
    ```
    spring.datasource.url = jdbc:postgresql://localhost:5432/bookstore
    spring.datasource.username = postgres
    spring.datasource.password = password
    ```
- Create a databases named bank and bookstore if using default name using the following SQL commands: 
  ```
  CREATE DATABASE bank;
  CREATE DATABASE bookstore;
  ```


<div align="right">[ <a href="#table-of-contents">↑ Back to top ↑</a> ]</div>

## Usage

**Running the bookstore app**
  - Front end:
    - Open a terminal or command prompt
    - Navigate to the *bookstore-frontend/bookstore* directory
    - Run `npm install` to install the required dependencies
    - Start the React server by running `npm start`
  - Back end:
    - Open a terminal or command prompt
    - Navigate to the *bookstore-backend/bookstore-backend>* directory
    - Run `mvn package` to compile Java application
    - Start the Java application by running `java -jar .\target\<application-name>.jar` replacing `<application-name>.jar` with the actual name of the JAR file
  
**Running the bank app**
  - Front end:
    - Open a terminal or command prompt
    - Navigate to the *Bank/frontend* directory
    - Run `npm install` to install the required dependencies
    - Start the React server by running `npm start`
  - Back end:
    - Open a terminal or command prompt
    - Navigate to the *Bank/Backend* directory
    - Run `mvn package` to compile Java application
    - Start the Java application by running `java -jar .\target\<application-name>.jar` replacing `<application-name>.jar` with the actual name of the JAR file
<div align="right">[ <a href="#table-of-contents">↑ Back to top ↑</a> ]</div>

## Authors

[![Contributors image](profile/images/contributors.svg)](https://github.com/SBNZ-SmFoYcSNaQ/Bank/graphs/contributors)
<div align="right">[ <a href="#table-of-contents">↑ Back to top ↑</a> ]</div>
