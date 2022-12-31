# Behavioral Interview Questions

__Interviewer__

__1. Tell me about yourself__

My mission in life is to bring people together and realize greatness on a community & personal level.

My 4-core values, which align well with BetMgM's stated cultural tenets are:

1. choose enduring greatness

2. do whatever you can to produce the desired results

3. be committed to improvement

4. insist on shared core values

SIMILARITIES

Do what is right = choose enduring long-term greatness
Hustle Hard = do whatever you can to produce the desired results & be committed to improvement
Backed By the Best = insist on shared core values"

I train in the evenings & perform on the weekends as a latin dancer with the very achievable goal of becoming a multi-world champion.

__What you'd like to learn in the role__

I would like to learn how to manage and grow an enterprise-level business with decisions based on data analytics.

__2a. Why do you want to work here specifically?__

I want to work at __BetMgM__ specifically because:

One, the Strategy & Planning role intrigues me: It seems like an ideal entry point for career opportunities that balance both my technology and business interests. While I was doing my research into your company I noticed that your company doesn't currently offer sports betting on Competitive Latin Dance, the prospect of potentially leading that initiative down the road excites me.

Two, per Glassdoor reviews, you score high on collaborative culture and Adam Greenblatt's CEO leadership. I've learned through experience & reading, that no one achieves enduring greatness alone, which is what I want. Thus, insisting on surrounding myself with other people that share the same core values is paramount.

__3. How do your previous experiences correlate to this specific position?__

My experience as an international box-office coordinator at Lionsgate, taught me the importance of having built-in quality assurance checks when creating & updating financial models based on local sales data from our international distributors. Prior to that, I also served as an executive assist to their then-president of Motion Picture, Erik Feig, managing his calendar and taking meeting notes.

As an SE at Choice Hotels, not only did I hone my technical skills & understanding, but I gained first-hand exposure to macro product management by implementing user stories. As an SE that adhered to the Agile Scrum methodology, I built up experience with Content Management Systems & Project Management Tools  to guide features from inception to Test Driven Development implementation to production deployment.

__4. What CMS (content management system) experience do you have?__

Based off what I am learning in this Google Digital Marketing course I'm taking, I recently built and deployed an SEO website using WIX to build up my nascent side-hustle business of teaching private salsa dance lessons.

On an enterprise-level, I regularly used Bitbucket when I was running production Jenkin & AWS deployments every-other week (We were migrating from on-premise to the cloud, thus 2 deployments). When I was on production trouble-shooting calls, I routinely checked that all the information was properly entered in our CMS to make sure our API calls would work properly. Thankfully, my team and I routinely documented all of our findings in Confluence for future reference.

__5. What project management tools do you have experience with?__

For some personal projects, I've used Trello's Kanban Board with a waterfall project management approach to define to-do, doing, & done phases. For my latest on-going Java project - A music manager TDD app demonstrating how Java can interface with a SQL database -- I simply used Github and am using my Readme file as PR request & Kanban board.

As an enterprise SE, I used Atlassian's Jira to track progress on user stories during a sprint and Bitbucket as version control.

__6. What are your current salary requirements?__

Given my technical background, 70K-80K dollars a year would be fair.

# End of Interview Questions


# Technical Interview Questions

__Q1__

Given a signed 32-bit integer x, return x with its digits reversed

- if reversing x causes it to go outside the signed 32-bit integer range, return 0

- assume env does not allow 64-bit integers

TIME COMPLEXITY
O(1) linear: dependent length of n

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

@Test
void reversed_positiveInput() {
    int input = 123;

    int expected = 321;
    int actual = Q1.reversed(input);
    assertEquals(expected, actual);
}

@Test
void reversed_negativeInput() {
    int testInput = -123;

    int expected = -321;
    int actual = Q1.reversed(input);
    assertEquals(expected, actual);
}

public static int reversed(int x) {

    boolean isNegative = false;
    int result = 0;

    if(x < 0) {
        x *= -1;
        isNegative = true;
    }

    result = recursion(x, result);

    if(isNegative) result *= -1;

    return result;
}

private static int recursion(int x, int result) {

    boolean isBaseCase = (x <= 0);

    if(isBaseCase) return 0;

    int lastDigit = x % 10;

    x /= 10;
    result = (result * 10) + lastDigit;

    return recursion(x, result);
}
```

__Q2__

write a program that outputs the string representation of a long number from 1 to n

- the method returns an arrayList of GENERIC CLASS strings

for multiples of:
- 3 it should return "Fizz" instead of the number
- 5 it should return "Buzz" instead of the number
- 5 AND 3 it should return "FizzBuzz" instead of the number

TIME COMPLEXITY
O(n) linear: dependent length of n

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

private static final String FIZZ = "Fizz";
private static final String BUZZ = "Buzz";
private static final String FIZZ_BUZZ = "FizzBuzz";

@Test
void fizzBuzz_0() {
    ArrayList<String> actualValues = Q2.fizzBuzz(-3);
    assertEquals(null, actualValues);
}

@Test
void fizzBuzz_3() {
    ArrayList<String> actualValues = Q2.fizzBuzz(3);
    ArrayList<String> expectedValues = new ArrayList<>();

    expectedValues.add("1");
    expectedValues.add("2");
    expectedValues.add(FIZZ);

    assertEquals(expectedValues, actualValues);
}

@Test
void fizzBuzz_5() {
    ArrayList<String> actualValues = Q2.fizzBuzz(5);
    ArrayList<String> expectedValues = new ArrayList<>();

    expectedValues.add("1");
    expectedValues.add("2");
    expectedValues.add(FIZZ);
    expectedValues.add("4");
    expectedValues.add(BUZZ);

    assertEquals(expectedValues, actualValues);
}

@Test
void fizzBuzz_3And5() {
    ArrayList<String> actualValues = Q2.fizzBuzz(15);
    ArrayList<String> expectedValues = new ArrayList<>();

    expectedValues.add("1");
    expectedValues.add("2");
    expectedValues.add(FIZZ);
    expectedValues.add("4");
    expectedValues.add(BUZZ);

    expectedValues.add(FIZZ);
    expectedValues.add("7");
    expectedValues.add("8");
    expectedValues.add(FIZZ);
    expectedValues.add(BUZZ);

    expectedValues.add("11");
    expectedValues.add(FIZZ);
    expectedValues.add("13");
    expectedValues.add("14");
    expectedValues.add(FIZZ_BUZZ);

    assertEquals(expectedValues, actualValues);
}

public static ArrayList<String> fizzBuzz(long number) {

    if(number < 1) return null;

    ArrayList<String> strings = new ArrayList<>();
    int i;

    while(i <= number) {

        boolean divBy5 = (i % 5 == 0);
        boolean divBy3 = (i % 3 == 0);

        if(divBy5 && divBy3) {

            strings.add("FizzBuzz");

        } else if(divBy3) {

            strings.add("Fizz");

        } else if(divBy5) {

            strings.add("Buzz");

        } else {
            strings.add(Long.toStrings(i));
        }

        i++;
    }

    return strings;
}
```

__Q3__

Given a square matrix mat, return the sum of the matrix diagonals.

- only include the sum of all the elements on the primary diagonal

- all the elements on the secondary diagonal that are not part of the primary diagonal.

Logic:

     length = width or height

     diagonal_1 = 1 + 5 + 9 = 15 = matrix[i][i]

     diagonal_2 = 3 + 5 + 7 = 15 = matrix[i][length - i - 1]

     matrix = [
           [1,2,3],
           [4,5,6],
           [7,8,9]
     ]

     remove duplicate 5 that appears in both diagonals from current sum 30
     diagonal_sum = 25

     step 1a: define index of traversing row
     step 1b: define index of shifting diagonal

     step 2: add to sum

     step 3: iterate over rows repeating process

     step 4: remove duplicate middle element from sum if matrix length is odd

     step 5: return sum

TIME COMPLEXITY
O(n) linear: where n is the length of the given array

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

@Test
void matrixDiagonalSum_success() {

    int[][] test = {
            {1,2,3},
            {4,5,6},
            {7,8,9}
    };

    int expected = 25;
    int actual = Q3.matrixDiagonalSum(test);
    assertEquals(expected, actual);
}

@test
matrixDiagonalSum_fail_badInput() {

    int[][] input = null;

    int expected = -1;
    int actual = Q3.matrixDiagonalSum(input);
    assertEquals(expected, actual);
}

public static int matrixDiagonalSum(int[][] matrix) {

    if(matrix == null || matrix.length == 0) return -1;

    int sum;

    // traverse rows
    for(int row = 0; row < matrix.length; row++) {

        // start index of second diagonal
        int diagonal = (matrix.length - 1) - row;

        int valueD1 = matrix[row][row];
        int valueD2 = matrix[row][diagonal];

        sum += (valueD1 + valueD2);
    }

    // remove duplicate middle element
    boolean isOddMatrixLength = (matrix.length % 2 != 0);

    if(isOddMatrixLength) {

        int middleIndex = matrix.length / 2;
        int middleValue = matrix[middleIndex][middleIndex];

        return sum - middleValue;
    }

    return sum;
}
```

__Q4__

Given an array of non-negative integers arr, you are initially positioned at start index of the array.

- When you are at index i, you can jump to:

```json

(i + arr[i]) || (i - arr[i])
```

- check if you can reach to any index with value 0.

- Notice that you can not jump outside the array at any time.

Logic:

- use Depth First Search (DFS) by using recursive functions calls for incrementing & decrementing start parameters
- its DFS because the method will handle one direction first and drill down for a base case
- before continuing to next recursive direction if necessary

DEPTH FIRST SEARCH: recursively, check if the currentNode has any children (left-to-right) that has the search path for the target node

- hasPath(s, t): recursively, nodeS do you have a path to nodeT?
- nodeS asks (left-to-right) it's child if it has a path to nodeT, repeat until reached nodeT or null

TIME COMPLEXITY
O(n) linear: worst-case, traverse the length of the input array size

SPACE COMPLEXITY
O(1) constant SPACE COMPLEXITY: in-place algorithm that doesn't require additional memory space

```json

@Test
jumpGame3_true() {

    int[] input = {4,2,3,0,3,1,2};
    int start = 5;
    boolean actual = Q4.jumpGame3(input, start);
    assertTrue(actual);
}

@Test
jumpGame3_fail_badInput() {

    int[] array = {};
    int start = -1;

    boolean actual = Q4.jumpGame3(array, start);
    assertFalse(actual);
}

public static boolean jumpGame3(int[] array, int start) {

    if(array.length == 0||
        start < 0 ||
        start >= (array.length - 1)
    ) return false;

    int currentElement = array[start];

    boolean isBaseCase = (currentElement == 0);

    if(isBaseCase) return true;

    int incrementedStart = start + currentElement;
    int decrementedStart = start - currentElement;

    // depth-first search
    return jumpGame3(array, incrementedStart) ||
        jumpGame3(array, decrementedStart);
}
```

__Q5__

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Logic:

- BACKTRACKING recursive algorithm

- RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)

choice:
- we can choose open "(" or close bracket ")"

constraint: we can choose close bracket if left <= right
- left = num open brackets
- right = num close brackets

goal:
- find (2 * max) valid parenthesis

TIME COMPLEXITY
O(n) linear: depending on longest string of two arguments

SPACE COMPLEXITY
O(1) constant: using an array

```
@Test
void generateParenthesis_success(){
    int test = 2;

    List<String> expected = new ArrayList<>();
    expected.add("(())");
    expected.add("()()");

    List<String> actual = Q5.generateParenthesis(test);
    assertEquals(expected, actual);
}

@Test
void generateParenthesis_fail(){
    int test = 1;

    List<String> expected = new ArrayList<>();
    expected.add("()");

    List<String> actual = Q5.generateParenthesis(test);
    assertEquals(expected, actual);
}

public static List<String> generateParenthesis(int number) {

    if(n <= 0) return null;

    List<String> maxValidParenthesis = new ArrayList<>();
    String currentParenthesis = "";

    int numLeftP = 0;
    int numRightP = 0;

    recursiveBacktracking(maxValidParenthesis, currentParenthesis, numLeftP, numRightP, number);

    return maxValidParenthesis;
}

private static void recursiveBacktracking(List<String> result, String currentParenthesis, int numOpenP, int numClosedP, int max) {

    int pSet = 2;
    int maxCombo = pSet * max;

    boolean isBaseCase = (currentParenthesis.length() == maxCombo);

    String pOpen = "(";
    String pClosed = ")";

    if(isBaseCase) {
        result.add(currentParenthesis);
        return;
    }

    // left-to-right
    if(numOpenP < max) {

        String addedOpenParenthesis = currentParenthesis + pOpen;
        int incrementedNumOpenP = numOpenP + 1;

        recursiveBacktracking(result, addedOpenParenthesis, incrementedNumOpenP, numClosedP, max);
    }

    if(numClosedP < numOpenedP) {

        String addedClosedParenthesis = currentParenthesis + pClosed;
        int incrementedNumClosedP = numClosedP + 1;

        recursiveBacktracking(result, addedClosedParenthesis, numOpenP, incrementedNumClosedP, max);
    }
}
```

__Q6__

read 10 numbers from the console entered by the user and print the sum of those 10 numbers

use input validation, if the input is not a number print the message 'Invalid Number'
    continue reading until you have read 10 numbers

```json

public class Q6 {

    public static final String INVALID_NUMBER = "Invalid Number";
    public static final String FINAL_SUM = "\nfinal sum: ".toUpperCase();
    public static final String ENTER_NUMBER = "\nEnter number: ";
    public static final String COMPLETED_TASK = "Completed Task";
    public static final String RUNNING_SUM = "running sum: ";

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.println(sumUserInput(scanner, 0, 0));
    }

    private static String sumUserInput(Scanner scanner, int count, int sum) {

        // ! RECURSIVE BASE CASE: breaking condition that initiates an upward propagation of return values for waiting stack calls
        boolean isBaseCase = (count == 3);

        if(isBaseCase) {

            scanner.close();
            System.out.println(FINAL_SUM + sum);
            return COMPLETED_TASK;
        }

        System.out.println(ENTER_NUMBER);

        if(scanner.hasNextInt()) {

            sum += scanner.nextInt();

            System.out.println(RUNNING_SUM + sum);
            count++;

        } else {
            System.out.println(INVALID_NUMBER);
        }

        return sumUserInput(new Scanner(System.in), count, sum);
    }
}
```

__Q7__

Demonstrate Object-Oriented Programming (OOP) by defining a Song, Album, and Playlist class that work in concert with each other.

Song(String title, Double duration)

Album(String name, String artist, ArrayList<Song> songs)

- addSong(String title, double duration)
- addToPlaylist(int trackNumber, LinkedList<Song> playlist)
- addToPlaylist(String title, LinkedList<Song> playlist)
- findSong(String title)

Playlist = Doubly LinkedList class

- play();
- printList();
- printMenu()

```json

public static void main(String[] args) {

}

public class Playlist {

    // CONSTANTS: static class variables assigned FINAL value before compilation/instantiation
    private static final String MENU =
        "\n\tPlaylist Menu\n".toUpperCase() +
        "0 - quit\n" +
        "1 - next song\n" +
        "2 - previous song\n" +
        "3 - replay current song\n" +
        "4 - list playlist songs\n" +
        "5 - print available actions\n" +
        "6 - delete current song from playlist\n";

    private static final String CURRENTLY_PLAYING = "Currently playing: ";
    private static final String INVALID_INPUT = "Invalid input";
    private static final String NO_SONGS = "No songs in playlist";
    private static final String PLAYLIST_BEGINNING = "Playlist beginning";
    private static final String PLAYLIST_COMPLETE = "Playlist complete";
    private static final String REPLAYING = "Now replaying: ";
    private static final String SELECTION = "\nSelection: ";
    private static final String SONG_REMOVED = " - song in playlist has been removed";

    // OOP ENCAPSULATION private class fields
    private String name;

    // OOP CONSTRUCTOR that initializes the class fields on class/object instantiation
    public Playlist(String name) {
        this.name = name;
    }

    // CLASS METHODS
    private static void printMenu() {
        System.out.println(MENU);
    }

    // STATIC: methods or variables associated with the class blueprint and not any individual instance and saved in a single place in memory
    private static void printList(LinkedList<Song> playlist) {

        // GENERIC CLASS: improve ENCAPSULATION by enforcing specific dataType parameters
        ListIterator<Song> songIterator = playlist.listIterator();

        while(songIterator.hasNext()) {
            System.out.println(songIterator.next().toString());
        }
    }

    public static void play(LinkedList<Song> playlist) {

        Scanner scanner = new Scanner(System.in);
        boolean quit = false;
        boolean isForwardProgression = true;

        // define listIterator for navigational linkedList
        ListItarator<Song> songListIterator = play.listIterator();

        if(playlist.size() <= 0) {

            System.out.println(NO_SONGS);
            return;

        } else {

            // iterate.next() to first node (Song, nextPointer)
            System.out.println(
                CURRENTLY_PLAYING +
                songListIterator.next().toString()
            );
        }

        printMenu();

        while(!quit) {

            System.out.println(SELECTION);

            if(scanner.hasNextInt()) {

                int choice = scanner.nextInt();

                // handle 'enter' key-down to capture user input
                scanner.nextLine();

                switch(choice) {
                    case 0:
                        System.out.println(PLAYLIST_COMPLETE);
                        quit = true;
                        break;

                    case 1: // move forward

                        // handle direction: if !forward, prepare direction as forward to next node
                        if(!isForwardProgression) {

                            // validate current pointer not null
                            if(songListIterator.hasNext()) {
                                songListIterator.next();
                            }

                            isForward = true;
                        }

                        // move to next node
                        if(songListIterator.hasNext) {

                            System.out.println(
                                CURRENTLY_PLAYING +
                                songListIterator.next().toString()
                            );

                        } else {
                            System.out.println(PLAYLIST_COMPLETE);
                            isForward = false;
                        }

                        break;

                    case 2: // move backward

                        // handle direction: if !forward, prepare direction as backward to next node
                        if(isForwardProgression) {

                            // validate current pointer not null
                            if(songListIterator.hasPrevious()) {
                                songListIterator.previous();
                            }

                            isForwardProgression = false;
                        }

                        // move to previous node in linkedList
                        if(songListIterator.hasPrevious()) {
                            System.out.println(
                                CURRENTLY_PLAYING + songListIterator.previous().toString()
                            );

                        } else {
                            System.out.println(PLAYLIST_BEGINNING);
                            isForwardProgression = true;
                        }
                        break;

                    case 3: // repeat

                        // handle direction: if forward, validate previous node & show

                        break;

                    case 4:
                        printList(playlist);
                        break;

                    case 5:
                        printMenu();
                        break;

                    case 6: // delete song

                        break;
                }

            } else {
                scanner = new Scanner(System.in);
                System.out.println(INVALID_INPUT);
                printMenu();
            }

        }
    }

    // OOP GETTERS & SETTERS
    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

public class Song {

    // OOP ENCAPSULATION private class fields/object instance members
    private String title;
    private Double duration;

    // OOP CONSTRUCTOR that initializes the class fields on class/object instantiation
    public Song(String title, Double duration) {
        this.title = title;
        this.duration = duration;
    }

    // OOP POLYMORPHISM: unique implementation of method for this object despite same signature shared by multiple objects via @Override
    @Override
    public String toString() {
        return this.title + ":" + this.duration;
    }

    // OOP GETTERS & SETTERS
    public String getTitle() {
        return this.title;
    }

    public Double getDuration() {
        return this.duration;
    }

    public void setDuration(double duration) {

        // AUTOBOXING: cast primitive dataType to greater functional wrapper class dataType
        this.duration = duration;
    }
}

public class AlbumTest {

    private static final String BEFORE_EACH = "before each".toUpperCase();
    private static final String OUI = "Oui";

    private Album album;

    @BeforeAll
    static void beforeAll() {
        System.out.println("before all".toUpperCase());
    }

    @BeforeEach
    void setup() {
        album = new Album("Live at Yankee Stadium", "Fania All-Stars");
        System.out.println(BEFORE_EACH);
    }

    @AfterEach
    void teardown() {
        System.out.println("after each".toUpperCase());
    }

    @AfterAll
    static void afterAll() {
        System.out.println("after all".toUpperCase());
    }

    @Test
    void album_findSong_success() {

        String testTitle = OUI;

        Song expected = new Song(testTitle, 239);
        Song actual = Album.findSong(testTitle);

        assertEquals(expected, actual);
    }

    @Test
    void album_findSong_null() {

        String testTitle = "Non-existent song";

        Song actual = Album.findSong(testTitle);

        assertNull(actual);
    }

    @Test
    void album_findSong_badInput() {

        String testTitle = "";

        Song actual = Album.findSong(testTitle);

        assertNull(actual);
    }

    @Test
    void album_addSong_true() {

        String testTitle = OUI;
        double testDuration = 239;

        boolean actual = Album.addSong(testTitle, testDuration);

        assertTrue(actual);
    }

    @Test
    void album_addSong_false() {

        String testTitle = "";
        double testDuration = 239;
        boolean actual = Album.addSong(testTitle, testDuration);

        assertFalse(actual);

        testTitle = OUI;
        testDuration = 0;
        actual = Album.addSong(testTitle, testDuration);

        assertFalse(actual);
    }

    @Test
    void album_addToPlayList1_true() {

        String testTitle = OUI;
        LinkedList<Song> testPlaylist = new LinkedList<>();

        boolean actual = Album.addToPlaylist(testTitle, testPlaylist);
        assertTrue(actual);
    }

    @Test
    void album_addToPlayList1_false() {

        String testTitle = "";
        LinkedList<Song> testPlaylist = new LinkedList<>();

        boolean actual = Album.addToPlaylist(testTitle, testPlaylist);
        assertFalse(actual);
    }

    @Test
    void album_addToPlayList2_true() {

        int testTrack = 0;
        LinkedList<Song> testPlaylist = new LinkedList<>();

        boolean actual = Album.addToPlaylist(testTrack, testPlaylist);
        assertTrue(actual);
    }

    @Test
    void album_addToPlayList2_false() {

        int testTrack = -1;
        LinkedList<Song> testPlaylist = new LinkedList<>();

        boolean actual = Album.addToPlaylist(testTrack, testPlaylist);
        assertFalse(actual);
    }
}

public class Album {

    // CONSTANTS static class variables assigned FINAL value before compilation/instantiation
    private static final String NO_ALBUM_TITLE = " album does not have the title ";
    private static final String NO_ALBUM_TRACK = " album does not have track ";

    // OOP ENCAPSULATION private class fields/object instance members
    private String name;
    private String artist;

    // GENERICS: improve OOP ENCAPSULATION by creating classes, interfaces, & methods that only take a specific dataType parameter
    private ArrayList<Song> songs;

    // OOP CONSTRUCTOR that initializes the class fields on class/object instantiation
    public Album(String name, String artist) {
        this.name = name;
        this.artist = artist;

        this.songs = new ArrayList<>();
    }

    // CLASS METHODS
    private Song findSong(String title) {

        if(title.length() == 0) return null;

        // for each song in Songs
        for(Song song: this.songs) {
            boolean hasSong = song.getTitle().equals(title);
            if(hasSong) return song;
        }
        return null;
    }

    public boolean addSong(String title, double duration) {

        if((title.length() == 0) || (duration <= 0) || (this.songs == null)) return false;

        if(findSong(title) == null) {

            Song newSong = new Song(title, duration);

            this.songs.add(newSong);
            return true;
        }
        return false;
    }

    // METHOD OVERLOADING: write multiple methods with the same name, but each have different parameters to optimize readability & scalability of the codebase
    public boolean addToPlaylist(String title, LinkedList<Song> playlist) {

        if(title.length() == 0 || playlist == null) return false;

        Song song = findSong(title);

        if(song != null) {
            playlist.add(song);
            return true;
        }

        System.out.println(this.getName() + NO_ALBUM_TITLE + track);
        return false;
    }

    public boolean addToPlaylist(int track, LinkedList<Song> playlist) {

        if(track < 0 || playlist == null) return false;

        int index = track - 1;

        boolean inAlbum = (index >= 0) && (index <= this.songs.size());

        if(inAlbum) {
            Song song = this.songs.get(index);
            playlist.add(song);
            return true;
        }

        System.out.println(this.getName() + NO_ALBUM_TRACK + track);
        return false;
    }

    // OOP GETTERS & SETTERS
    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getArtist() {
        return this.artist;
    }

    public void setArtist(String artist) {
        this.artist = artist;
    }

    public ArrayList<Song> getSongs() {
        return this.songs;
    }
}
```

__Q8__

```
/**
* ! instagram challenges
*
* * db schema:
*
* *   users:
*       id,
*       username (mandatory & one-of-a-kind),
*       created_at (current date & time)
* *   photos:
*       id,
*       image_url mandatory,
*       created_at,
*       user_id (mandatory & foreign key)
* *   comments:
*       id,
*       comment_text mandatory,
*       photo_id (foreign key),
*       created_at (current date & time),
*       user_id (foreign key),
* *   likes:
*       created_at (current date & time),
*       user_id (foreign key),
*       photo_id (foreign key),
*       primary key order: user_id & photo_id
* *   follows:
*       created_at (current date & time),
*       follow_id *foreign key,
*       followee_id *foreign key,
*       primary key order: user_id & photo_id
* *   tags:
*       id,
*       tag_name unique,
*       created_at (current date time)
* *   photo_tags:
*       photo_id (foreign key),
*       tag_id (foreign key),
*       primary key order: user_id & photo_id
*/
```

we want to reward our users who have been around the longest
find the 5 oldest users

```
SHOW DATABASES;
SELECT database();

USE ig_db;
SHOW TABLES;

DESC users;

SELECT
    *
FROM users
ORDER BY created_at DESC
LIMIT 5;
```

we need to figure out when to schedule an ad campaign
what day of the week do most users register on (labeled: most popular registration day)
get count and day name

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

__Q9__

```
/**
* ! query many-to-many table from created reviewers, series, review tables
*
* * reviewers schema:
* *    id,
* *    first_name (default 'MISSING' max 20 chars),
* *    last_name (default 'MISSING' max 20 chars)
*
* * series schema:
* *    id,
* *    title (default "MISSING" max 20 chars),
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
DESC series;
DESC reviews;

SELECT
    series.title,
    reviews.rating
FROM series
INNER JOIN reviews
    ON series.id = reviews.series_id
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
        2
    ) AS avg_rating
FROM series
INNER JOIN reviews
    ON series.id = reviews.series_id
GROUP BY series.id
ORDER BY AVG(reviews.rating) ASC
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
USE ig_db;

SHOW TABLES;
DESC reviewers;
DESC reviews;

SELECT
    IFNULL(
        reviewers.first_name,
        UPPER("missing")
    ),
    IFNULL(
        reviewers.last_name,
        UPPER("missing")
    ),
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
            AVG(reviews.rating), 2
        ),
        0.00
    ) AS UPPER("avg"),
    CASE
        WHEN AVG(reviews.rating) IS NULL
            THEN UPPER("inactive")
        WHEN AVG(reviews.rating) > 0 AND AVG(reviews.rating) < 10
            THEN UPPER("active")
        ELSE
            THEN UPPER("power user")
    END
FROM reviewers
LEFT JOIN reviews
    ON reviewers.id = reviews.reviewer_id
GROUP BY reviewers.id
ORDER BY UPPER("min") DESC
LIMIT 4;
```

__Q10__

given an integer n, return the number of trailing zeroes in n!

TIME COMPLEXITY: O(logn) logarithmic
SPACE COMPLEXITY: O(1) constant

```
public static Integer trailingZeroFactorial(int n) {

    if(n < 0) return -1;

    Integer nFactorial = n; // AUTOBOXING
    int everyFiveCount = 0

    while(nFactorial % 5 == 0) {

        nFactorial /= 5;

        // ex) 15 / 5 = there are 3 fives in 15
        everyFiveCount += nFactorial;
    }

    return everyFiveCount; // AUTOBOXING
}
```