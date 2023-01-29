# Behavioral Interview Questions

__Interviewer__

Name:

Title:

__1. Tell me about yourself__

My mission in life is to bring people together and realize greatness on a community & personal level.

My 4-core values, which align well with BetMgM's stated cultural tenets are:

1. choose enduring greatness

2. do whatever you can to produce the desired results

3. be committed to improvement

4. insist on shared core values

I train in the evenings & perform on the weekends as a latin dancer with the very achievable goal of becoming a multi-world champion.

__What you'd like to learn in the role__

I would like to learn how to manage and grow an enterprise-level business with decisions based on data analytics.

__2a. Why do you want to work here specifically?__

I want to work at __BetMgM__ specifically because:

One, the Strategy & Planning role intrigues me: It seems like an ideal entry point for career opportunities that balance both my technology and business interests. While I was doing my research into your company I noticed that your company doesn't currently offer sports betting on Competitive Latin Dance, the prospect of potentially leading that initiative down the road excites me.

Two, per Glassdoor reviews, you score high on collaborative culture and Adam Greenblatt's CEO leadership. I've learned through experience & reading, that no one achieves enduring greatness alone, which is what I want. Thus, insisting on surrounding myself with other people that share the same core values is paramount.

__3. How do your previous experiences correlate to this specific position?__

My experience as an international box-office coordinator at Lionsgate, taught me the importance of having built-in quality assurance checks when creating & updating financial models based on local sales data from our international distributors. Prior to that, I also served as an executive assist to their then-president of Motion Picture, Erik Feig, managing his calendar and taking meeting notes.

As an SE at Choice Hotels, not only did I hone my technical skills & understanding, but I gained first-hand exposure to macro product management by implementing user stories. As an SE that adhered to the Agile Scrum methodology, I built up experience with resources Management Systems & Project Management Tools  to guide features from inception to Test Driven Development implementation to production deployment.

__4. What CMS (resources management system) experience do you have?__

Based off what I am learning in this Google Digital Marketing course I'm taking, I recently built and deployed an SEO website using WIX to build up my nascent side-hustle business of teaching private salsa dance lessons.

On an enterprise-level, I regularly used Bitbucket when I was running production Jenkin & AWS deployments every-other week (We were migrating from on-premise to the cloud, thus 2 deployments). When I was on production trouble-shooting calls, I routinely checked that all the information was properly entered in our CMS to make sure our API calls would work properly. Thankfully, my team and I routinely documented all of our findings in Confluence for future reference.

__5. What project management tools do you have experience with?__

For some personal projects, I've used Trello's Kanban Board with a waterfall project management approach to define to-do, doing, & done phases. For my latest on-going Java project - A music manager TDD app demonstrating how Java can interface with a SQL database -- I simply used Github and am using my Readme file as PR request & Kanban board.

As an enterprise SE, I used Atlassian's Jira to track progress on user stories during a sprint and Bitbucket as version control.

__6. What are your current salary requirements?__

Given my technical background, 70K-80K dollars a year would be fair.

# End of Interview Questions


# EXCEL

```
=VLOOKUP(missing_table_cell_primary_key, fixed_reference_table, target_column_number_in_fixed_reference_table, is_exact_match)

- $ is fixed referenced table (to avoid reference movement when coping & pasting)
```

__Task 1: find the number of days in transit in the purchase table__

<img src="/resources/excel_vlookup_1.png" alt="excel vlookup 1">

```
SAME TABLE SOLUTION:

=VLOOKUP(store_cell_purchase_primary_key, fixed_reference_table, target_column_number_in_fixed_reference_table, is_exact_match)

=VLOOKUP(C3, $A$9:$C$13, 3, FALSE)
```

<img src="/resources/excel_vlookup_1_solution.png" alt="excel vlookup 1 solution">

__Task 2: find the "num kgs sold" & "billing agent" in the purchase table__

<img src="/resources/excel_vlookup_2a.png" alt="excel vlookup 2" alt="excel vlookup 2">

<img src="/resources/excel_vlookup_2b.png" alt="excel vlookup 2" alt="excel vlookup 2">

<img src="/resources/excel_vlookup_2c.png" alt="excel vlookup 2" alt="excel vlookup 2">

```
MULTI-TABLE SOLUTION:

=VLOOKUP(date_cell_purchase_primary_key, fixed_reference_table, target_column_number_in_fixed_reference_table, is_exact_match)

"number of kgs sold"
=VLOOKUP(D2, Dates!$A$1:$B$5, 2, FALSE)

"billing agent"
=VLOOKUP(D2, Agents!$A$1:$B$5, 2, FALSE)
```

<img src="/resources/excel_vlookup_2a_solution.png" alt="excel vlookup 2">

<img src="/resources/excel_vlookup_2b_solution.png" alt="excel vlookup 2">

__Task 3: find the "city names" & "development category" in the purchase table__

<img src="/resources/excel_vlookup_3.png" alt="excel vlookup 3">

```
MULTI-TABLE SOLUTION:

=VLOOKUP(city_dev_index_primary_key, 'external sheet'!_reference_table, data_column_reference_table, is_approximate_match)

- double click on the mini-box to auto-populate entire column
- reference should always be on the left side

"city names"
```

<img src="/resources/excel_vlookup_3_solution.png" alt="excel vlookup 3">

# SQL

```
/**
* ! instagram challenges
*
* * users:
*     id,
*     username (mandatory & one-of-a-kind),
*     created_at (current date & time)
* * photos:
*     id,
*     image_url mandatory,
*     created_at,
*     user_id (mandatory & foreign key)
* * comments:
*     id,
*     comment_text mandatory,
*     photo_id (foreign key),
*     created_at (current date & time),
*     user_id (foreign key),
* * likes:
*     created_at (current date & time),
*     user_id (foreign key),
*     photo_id (foreign key),
*     primary key order: user_id & photo_id
* * follows:
*     created_at (current date & time),
*     follow_id foreign key,
*     followee_id foreign key,
*     primary key order: follow_id, followee_id
* * tags:
*     id,
*     tag_name mandatory unique,
*     created_at (current date time)
* * photo_tags:
*     photo_id (foreign key),
*     tag_id (foreign key),
*     primary key order: photo_id, tag_id
*/
```

```
SHOW DATABASES;
SELECT database();

CREATE DATABASE ig;
USE ig;

CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(20) NOT NULL UNIQUE,
    created_at DATETIME DEFAULT NOW()
);

DESC users;

CREATE TABLE photos(
    id INT AUTO_INCREMENT PRIMARY KEY,
    image_url VARCHAR(100) NOT NULL,
    created_at DATETIME DEFAULT NOW(),
    user_id INT,
    FOREIGN KEY(user_id)
        REFERENCES users(id)
        ON DELETE CASCADE
);

DESC photos;

CREATE TABLE comments(
    id INT AUTO_INCREMENT PRIMARY KEY,
    comment_text VARCHAR(255),
    created_at DATETIME DEFAULT NOW(),
    photo_id INT,
    user_id INT,
    FOREIGN KEY(photo_id)
        REFERENCES photos(id)
        ON DELETE CASCADE,
    FOREIGN KEY(user_id)
        REFERENCES users(id)
        ON DELETE CASCADE
);

DESC comments;

CREATE TABLE likes(
    created_at DATETIME DEFAULT NOW(),
    user_id INT,
    photo_id INT,
    FOREIGN KEY(user_id)
        REFERENCES users(id)
        ON DELETE CASCADE,
    FOREIGN KEY(photo_id)
        REFERENCES photos(id)
        ON DELETE CASCADE,
    PRIMARY KEY(user_id, photo_id)
);

DESC likes;

CREATE TABLE follows(
    created_at DATETIME DEFAULT NOW(),
    follow_id INT,
    followee_id INT,
    FOREIGN KEY(follow_id)
        REFERENCES users(id)
        ON DELETE CASCADE,
    FOREIGN KEY(followee_id)
        REFERENCES users(id)
        ON DELETE CASCADE,
    PRIMARY KEY(follow_id, followee_id)
);

DESC follows;

CREATE TABLE tags(
    id INT AUTO_INCREMENT PRIMARY KEY,
    tag_name VARCHAR(20) NOT NULL UNIQUE,
    created_at DATETIME DEFAULT NOW()
);

DESC tags;

CREATE TABLE photo_tags(
    photo_id INT,
    tag_id INT,
    FOREIGN KEY(photo_id)
        REFERENCES photos(id)
        ON DELETE CASCADE,
    FOREIGN KEY(tag_id)
        REFERENCES tags(id)
        ON DELETE CASCADE,
    PRIMARY KEY(photo_id, tag_id)
);

DESC photo_tags;
SHOW TABLES;
```

__we want to reward our users who have been around the longest find the 5 oldest users__

```
SHOW DATABASES;
SELECT database();

USE ig_db;
SHOW TABLES;

DESC users;

SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 5;
```

__we need to figure out when to schedule an ad campaign what day of the week do most users register on (labeled: most popular registration day) get count and day name__

```
SHOW DATABASES;
SELECT database();
USE ig_db;

SHOW TABLES;
DESC users;

SELECT
    *
FROM users
GROUP BY DAYNAME(created_at)
ORDER BY COUNT(*) DESC
LIMIT 1;

SELECT
    DAYNAME(created_at) AS "most popular registration day",
    COUNT(*) AS total
FROM users
GROUP BY DAYNAME(created_at)
ORDER BY total DESC
LIMIT 1;
```

we want to target our inactive users with an email campaign
find the users who have never posted a photo

```
SHOW DATABASES
SELECT database();
USE ig_db;

SHOW TABLES;
DESC users;
DESC photos;

SELECT
    users.username AS "inactive user"
FROM users
LEFT JOIN photos
    ON users.id = photos.user_id
WHERE photos.id IS NULL;
```

we're running a new contest to see
who can get the most likes on a single photo,
which user, photo, and like count won?

```
SHOW DATABASES;
SELECT database();
USE ig_db;

DESC users;
DESC photos;
DESC likes;

SELECT
    users.username,
    photos.image_url,
    COUNT(*) AS total
FROM users
INNER JOIN photots
    ON users.id = photos.user_id
INNER JOIN likes
    ON photos.id = likes.photo_id
GROUP BY photos.id
ORDER BY total DESC
LIMIT 1;
```

our investors want to know,
how many times does the average user post?
labeled as 'average number of posts'

```
SHOW DATABASES;
SELECT database();

USE ig_db;
SHOW TABLES;

DESC users;
DESC photos;

SELECT (
    SELECT COUNT(*) FROM photos / SELECT COUNT(*) FROM users
) AS "average number of posts";
```

our brand advertisers want to know which hashtags to use in a post,
what are the top 5 most commonly used hashtags
and the 5 highest count label as 'total'

```
SHOW DATABASES;
SELECT database();

USE ig_db;
SHOW TABLES;

DESC tags;
DESC photo_tags;

SELECT
    tags.tag_name,
    COUNT(*) AS total
FROM tags
INNER JOIN photo_tags
    ON tags.id = photo_tags.tag_id
GROUP BY tags.id
ORDER BY total DESC
LIMIT 5;
```

we have a small problem with bots on our site,
find users who have liked every single photo on the site

```
SHOW DATABASES;
SELECT database();

USE ig_db;
SHOW TABLES;

DESC users;
DESC photos;
DESC likes;

SELECT
    users.id
    users.username,
    COUNT(*) AS "max likes"
FROM users
INNER JOIN likes
    ON users.id = likes.user_id
GROUP BY users.id
HAVING "max likes" = (
    SELECT
        COUNT(*) AS "total_likes"
    FROM likes
    ORDER BY "total_likes" DESC
    LIMIT 1
);
```

```
/**
* ! query many-to-many table from created reviewers, series, review tables that uses prep data for respective table
*
* * imdb database
*
* * reviewers schema:
* *    id,
* *    first_name (mandatory default 'MISSING' max 20 chars),
* *    last_name (mandatory default 'MISSING' max 20 chars)
*
* * series schema:
* *    id,
* *    title (mandatory default "MISSING" max 20 chars),
* *    released_year (4-digit mandatory),
* *    genre (max 100 chars)
*
* * reviews schema:
* *    id,
* *    rating (MIN 0.0 to MAX 9.9),
* *    series_id,
* *    reviewer_id
*
* * on delete cascade many-to-many relationships
*/

SHOW DATABASES;

CREATE DATABASE imdb;
USE imdb;

CREATE TABLE reviewers(
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(20)  NOT NULL DEFAULT "MISSING",
    last_name VARCHAR(20) NOT NULL DEFAULT UPPER("missing")
);

DESC reviewers;

CREATE TABLE series(
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(20) NOT NULL DEFAULT UPPER("missing"),
    released_year YEAR(4) NOT NULL,
    genre VARCHAR(100)
);

DESC series;

CREATE TABLE reviews(
    id INT AUTO_INCREMENT PRIMARY KEY,
    rating DECIMAL(2, 1) NOT NULL,
    series_id INT,
    reviewer_id INT,
    FOREIGN KEY(series_id)
        REFERENCES series(id)
        ON DELETE CASCADE,
    FOREIGN KEY(reviewer_id)
        REFERENCES reviewers(id)
        ON DELETE CASCADE
);

DESC reviews;
SHOW TABLES;
```

challenge 1: reproduce the table below (no nulls):

```
title | rating

   archer | 8.0
   archer | 7.5
   arrested development | 8.9
   arrested development | 9.9
```

```
SHOW DATABASES;
SELECT database();
USE imdb;

SHOW TABLES;
DESC reviews;
DESC series;

SELECT
    series.title,
    reviews.rating
FROM reviews
INNER JOIN series
    ON reviews.series_id = series.id
ORDER BY series.title ASC
LIMIT 4;
```

challenge 2: reproduce the table below (no nulls):

```
title | avg_rating

    General Hospital | 5.38
    Fargo | 9.40
    Halt and Catch Fire | 9.90
```

```
SHOW DATABASES;
SELECT database();
USE imdb;

SHOW TABLES;
DESC series;
DESC reviews;

SELECT
    series.title,
    ROUND(
        AVG(reviews.rating),
        3
    ) AS "avg_rating"
FROM reviews
INNER JOIN series
    ON reviews.series_id = series.id
ORDER BY series.id
ORDER BY avg_rating ASC
LIMIT 3;
```

challenge 3: reproduce the table below (no nulls):

```
first_name | last_name | rating

    Thomas | Stoneman | 8.0
    Wyat | Skaggs | 8.5
    Wyat | Skaggs | 7.5
    Wyat | Skaggs | 9.3
    Kimbra | Masters | 7.1
```

```
SHOW DATABASES;
SELECT database();
USE imdb;

SHOW tables;
DESC reviewers;
DESC reviews;

SELECT
    reviewers.first_name,
    reviewers.last_name,
    reviews.rating
FROM reviewers
INNER JOIN reviews
    ON reviewers.id = reviews.reviewer_id
ORDER BY reviewers.last_name DESC
LIMIT 5;
```

challenge 4: reproduce the table below (there will be nulls):

```
unreviewed_series

    Malcolm in the Middle
    Pushing Daisies
```

```
SHOW databases;
SELECT database();
USE imdb;

SHOW TABLES;
DESC series;
DESC reviews;

SELECT
    series.title AS "unreviewed_series"
FROM series
LEFT JOIN reviews
    ON series.id = reviews.series_id
WHERE reviews.rating IS NULL
LIMIT 2;
```

challenge 5: reproduce the table below (there will be nulls):

```
genre | avg_rating

     Animation | 7.86
     Comedy | 8.16
     Drama | 8.04
```

```
SHOW DATABASES;
SELECT database();
USE imdb;

SHOW TABLES;
DESC series;
DESC reviews;

SELECT
    series.genre,
    IFNULL(
        ROUND(
            AVG(reviews.rating),
            2
        ),
        0
    ) AS "avg_rating"
FROM series
LEFT JOIN reviews
    ON series.id = reviews.series_id
GROUP BY series.genre
ORDER BY series.genre ASC
LIMIT 3;
```

challenge 6: reproduce the table below (there will be nulls):

```
    first_name | last_name | COUNT | MIN | MAX | AVG | STATUS

    thomas  | stoneman | 5  | 7.0  | 9.5 | 8.02 | ACTIVE
    wyatt   | skaggs   | 9  | 5.5  | 9.3 | 7.80 | ACTIVE
    colt    | steele   | 10 | 4.5  | 9.9 | 8.77 | POWER USER
    marlon  | crafford | 0  | 0    | 0   | 0.00 | INACTIVE
```

```
SHOW DATABASES;
SELECT database();
USE imdb;

SHOW TABLES;
DESC reviews;
DESC reviewers;

SELECT
    reviewers.first_name,
    reviewers.last_name,
    IFNULL(
        COUNT(reviews.id),
        0
    ) AS UPPER("count"),
    IFNULL(
        MIN(reviews.rating),
        0.0
    ) AS UPPER("min"),
    IFNULL(
        MAX(reviews.rating),
        0.0
    ) AS UPPER("max"),
    IFNULL(
        ROUND(
            AVG(reviews.rating),
            2
        ),
        0.00
    ) AS UPPER("avg")
    CASE
        WHEN AVG(reviews.rating) IS NULL OR AVG(reviews.rating) <= 0
            THEN UPPER("inactive")
        WHEN AVG(reviews.rating) > 0 AND AVG(reviews.rating) < 10
            THEN UPPER("active")
        ELSE
            THEN UPPER("power user")
    END
FROM reviewers
LEFT JOIN reviews
    ON reviewers.id =  reviews.reviewer_id
GROUP BY reviewers.id
ORDER BY UPPER("min") DESC
LIMIT 4;
```

challenge 7: reproduce the table below (no nulls):

```
    title | rating | reviewer

    archer | 8.0 | thomas stoneman
    archer | 7.0 | domingo cortes
    archer | 8.5 | kimbra masters
    arrested development | 8.4 | pinkie petit
    arrested development | 9.9 | colt steele
    bobs burgers | 7.0 | thomas stoneman
```

```
SHOW DATABASES;
SELECT database();
USE imdb;

SHOW TABLES;
DESC series;
DESC reviews;
DESC reviewers;

SELECT
    series.title,
    reviews.rating,
    CONCAT(
        reviewers.first_name, " ", reviewers.last_name
    ) AS "reviewer"
FROM reviews
INNER JOIN series
    ON reviews.series_id = series.id
INNER JOIN reviewers
    ON reviews.reviewer_id = reviewers.id
ORDER BY series.title ASC
LIMIT 6;
```

__Q11__

```
/**
* * school database
*
* * students schema:
* *    id primary key,
* *    first_name mandatory default "MISSING"
*
* * papers schema:
* *    id primary key,
* *    title 100 max chars mandatory,
* *    grade INT not mandatory,
* *    student_id INT,
* *    foreign key (student_id)
*/
```

```
SHOW DATABASES;
SELECT database();

CREATE DATABASE school;
USE school;

CREATE TABLE students(
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(20) NOT NULL DEFAULT UPPER("missing")
);

DESC students;

CREATE TABLE papers(
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    grade INT,
    student_id INT,
    FOREIGN KEY(student_id)
        REFERENCES students(id)
        ON DELETE CASCADE
);

DESC papers;
SHOW TABLES;
```

get
student id, first_name, title, grade,
by student id of the respective paper
and order by paper's grade highest-to-lowest

```
SHOW DATABASES;
SELECT database();
USE school;

SHOW TABLES;
DESC students;
DESC papers;

SELECT
    students.id,
    students.first_name,
    papers.title,
    papers.grade
FROM students
INNER JOIN papers
    ON students.id = papers.student_id
ORDER BY papers.grade DESC
```

# Java

```
public class TestStrings {

    // CONSTANTS/static class variables assigned final value before compilation/instantiation
    public static final String BEFORE_ALL = "Before all tests";
    public static final String BEFORE_EACH = "Before each test";
    public static final String AFTER_EACH = "After each test";
    public static final String AFTER_ALL = "After all tests";
    public static final String INVALID_VALUE = "Invalid Value";
    public static final String NOT_IMPLEMENTED_FAIL = "This test is failing because it hasn't been implemented yet";
}

// OOP INHERITANCE: child subclass inherits public class fields + methods from extending parent super class
public class PracticeTest extends TestStrings {

    // OOP ENCAPSULATION: use private access modifiers to guard the class fields & methods methods from inappropriate external access
    private Practice practice;

    @BeforeAll
    static void beforeAll() {
        System.out.println(BEFORE_ALL);
    }

    @BeforeEach
    void setUp() {
        System.out.println(BEFORE_EACH);
        practice = new Practice();
    }

    @AfterEach
    void tearDown() {
        System.out.println(AFTER_EACH);
    }

    @AfterAll
    static void afterAll() {
        System.out.println(AFTER_ALL);
    }

    @Test
    void findSingle_badInput() {
        int[] testInput = {};

        int actual = practice.findSingle(testInput);
        int expected = -1;
        assertEqual(actual, expected);
    }

    @Test
    void findSingle_alternatingInput() {
        int[] testInput = {4,1,2,1,2};

        int actual = practice.findSingle(testInput);
        int expected = 4;
        assertEqual(actual, expected);
    }

    @Test
    void findSingle_repeatingInput() {
        int[] testInput = {2,2,1};

        int actual = practice.findSingle(testInput);
        int expected = 1;
        assertEqual(actual, expected);
    }

    @Test
    void findSingle_singleInput() {
        int[] testInput = {1}

        int actual = practice.findSingle(testInput);
        int expected = 1;
        assertEqual(actual, expected);
    }

    @Test
    void reverseString_badInput() {

        String testInput = "";

        String actual = practice.reverseString(testInput);
        assertNull(actual);
    }

    @Test
    void reverseString_success() {

        String testInput = "abcde";

        String actual = practice.reverseString(testInput);
        String expected = "edcba";
        assertEqual(expected, actual);
    }

    @Test
    void reverseString_fail() {

        String testInput = NOT_IMPLEMENTED_FAIL;

        String actual = practice.reverseString(testInput);
        String expected = INVALID_VALUE;
        assertNotEquals(expected, actual);
    }
}
```

```
public class Practice extends TestStrings {

    /**
     * ? LeetCode 136: Amazon
     *
     * ? Given a non-empty array of integers (numbers), every element appears twice except for one. Find the single unique element.
     *
     * ? You must implement a solution with a linear runtime complexity and use only constant extra spit.
     *
     * * Logic:
     *      ! use XOR operator: for two same bits, results in 0
     *      XOR = ^
     *
     *      [2,2,1]
     *
     *          2 ^ 2 = 0
     *          0 ^ 1 = 1
     *
     *          return 1
     *
     * * O(n) linear TIME COMPLEXITY:
     * worst-case, the number of steps is directly proportional to the length of the input size because getting a value WITHOUT a key will require traversing to the end of a collection
     *
     * * O(1) constant TIME COMPLEXITY:
     * worst-case, getting a value with a key will always take the same number of steps (3)
     *
     */
    public int findSingle(int[] numbers) {

        // EXCEPTION HANDLING look before you leap: use if-else statement to handle exceptions
        if numbers.length == 0) return -1;

        int uniqueNumbers = numbers[0];

        for(int i = 1; i < numbers.length; i++) {
            uniqueNumbers = uniqueNumbers ^ numbers[i];
        }

        return uniqueNumbers;
    }

    /**
     * ? LeetCode 344:
     *
     * ? Write a function that reverses a String.
     *
     * ? The function is given a string of characters & returns a reversed String.
     *
     * ! O(n) linear TIME COMPLEXITY:
     * worst-case, the number of steps is directly proportional to the length of the input size because getting a value WITHOUT a key will require traversing to the end of a collection
     *
     * ! O(1) constant SPACE COMPLEXITY: o(1) since it's happening in place
     * worst-case, getting a value with a key will always take the same number of steps (3)
     *
     */
     public String reverseString(String input) {

        // EXCEPTION HANDLING look before you leap: use if-else statement to handle exceptions
        if(input.length == 0) return null;

        char letter = ' ';
        String result = "";
        int lastLetterIndex = input.length() - 1;

        for(int i = lastLetterIndex; i >= 0; i--) {
            letter = input.charAt(i);
            result += letter;
        }

        return result;
     }


}
```