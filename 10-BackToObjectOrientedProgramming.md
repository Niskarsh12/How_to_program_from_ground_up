# Back-to Object Oriented Programming Style (1980s-Present) <a name="boop"></a>
  - ### BIG IDEA #1 — The state of the program is immutable and is only changed by creating a totally new state by modifying the old state.
  - ### BIG IDEA #2 - The state of the objects is private and only mutable via methods that are called on the object.  

## Alan Kay Style BOOP (The _Original_ Object Oriented Programming)
  - Based on the idea of "messaging" between objects, VERY poorly named "object oriented programming", admitted 
    by Alan Kay himself, the inventor of the term.
    
    > [<img src="assets/alan_kay.png" width="320"/>](assets/alan_kay.png)
    > - Alan Kay at OOPSLA 1997 - The computer revolution hasn't happened yet
    >   - https://www.youtube.com/watch?v=oKg1hTOQXoY
    >> ### Alan Kay:
    >> - **"I'm sorry that I long ago coined the term “objects” for this topic because it gets many people to focus on the lesser idea."** 
    >> - The big idea is “messaging.” 
    >> - The key in making great and growable systems is much more to have things communicate through _messages_ and not through direct mutable state.
    
  - ### BOOP style takes the message metaphor to mean that the state of the program is immutable except by sending a message to create a new state.
    - The `object` state can only changed by creating a new state via modifying the old state by calling `public` 
      method on objects.
    - All state of the `object` is `private` and only accessible via methods that are called on the object.
  
      > - Alan Kay, 2015: Power of Simplicity
      >   - https://www.youtube.com/watch?v=NdSD07U5uBs
      >
      > - Rethinking CS Education | Alan Kay, CrossRoads 2015
      >   - https://www.youtube.com/watch?v=N9c7_8Gp7gI
      >
      > - We Were So Lucky Alan Kay
      >   - https://www.youtube.com/watch?v=ktPCH_p80e4
      >
      > - Seminar with Alan Kay on Object Oriented Programming (VPRI 0246)
      >   - https://www.youtube.com/watch?v=QjJaFG63Hlo
  
  - All state is fully retained in the `object` and methods are used to "send messages" to the `object` to
    change its state. This "messaging" metaphor stands up because internal state is not directly accessible. You
    must politely ask the object to change its state, and the object can choose to respond to the message or not.
    Unlike in COP where internal state is routinely exposed and directly manipulated via `static` methods and variables.
  - Any state of the object is exposed only via "messages", or method calls on the object, and the object can choose to respond to
    the message or not.
  - No `static` methods or variables, only instance variables that are private to the `object`.
    - Use of `static` methods and variables is specifically disallowed as it leads to "shared mutable state" and
      "side effects" that are difficult to maintain and understand.
      > Objects vs. Static Methods
      >   - https://www.youtube.com/watch?v=D0dqC_3Bch8
  - `protected` methods are allowed, but discouraged as they lead to "fragile" and "rigid" code.
  - Use of inheritance is explicitly discouraged, and prefer composition over inheritance. Exceptions for shallow
    hierarchies of 2-3 levels maximum meant to model the real world objects, not to create a "hierarchy of types."
  - Use of interfaces is limited to Classes that require testing, and are not automatically added for every class.
  - Use of `setters` and `getters` is specifically disallowed. Instead, the object is expected to respond to messages to change its
    state, and to respond to messages to get its state.
   
  - There are only a few true BOOP languages, "Smalltalk," "Ruby," and, _incredibly_, "Javascript" are among the most popular ones.

## Banned COP Patterns in BOOP <a name="banned-patterns-in-boop"></a>
 - ###### banned-patterns-in-boop
   > [<img src ="assets/yegor_bugayenko.png" width="300"/>](https://www.yegor256.com/about-me.html)
   > - [Yegor Bugayenko, Author of Elegant Objects](https://www.yegor256.com/about-me.html)
   > - BOOP is my name for the style of programming that Yegor Bugayenko describes in his book "Elegant Objects."
   > - What's Wrong With Object-Oriented Programming? Yegor Bugayenko
   >   - https://www.youtube.com/watch?v=K_QEOtYVQ7A
  
 - ### Specific COP-like "Design Patterns" are *NOT* permitted, such as:
   - Factory Pattern
   - Abstract Factory Pattern
   - Adapter Pattern is strongly discouraged, and prefer composition over inheritance.
   - Facade, Bridge, Proxy and Decorator Patterns are all very similar to the Adapter Pattern and are discouraged.
   - Builder Pattern considered too clumsy, the "Fluent" pattern is preferred 
     - "Fluent Pattern" is where an `object` is modified and returned to the caller to allow for "method chaining."
   - Type-casting is frowned upon, and prefer the use of interfaces or composition as type-casting was only necessary 
     for COP style implementations. 

     > - 10 Design Patterns Explained in 10 Minutes
     >   - https://www.youtube.com/watch?v=tv-_1er1mWI
     > - Patterns, Anti-Patterns, and Refactoring - Yegor Bugayenko
     >   - https://www.youtube.com/watch?v=LrTBIcFhawI
 
 - ### Other disallowed patterns common in COP:
   - Use of `null`
   - Use of `static` methods and variables
   - `Get`-ters and `Set`-ters
   - Reflection & Type Casting
   - Inheritance more than 2-3 levels deep. Prefer no inheritance and use composition instead.
   - Mutable State - All state in BOOP is immutable, and the object is expected to return a new object with the new state.
   - Classes ending with -er that mutate data passed in without retaining state internal to the object.
     - Like `Manager`, `Controller`, `Handler`, `Processor`, `Updater`, `Setter`, `Getter`, `Modifier`, `Changer`, etc.
 - Amazingly, the dreaded Singleton Pattern _is allowed_ to manage global state in BOOP, but not `static` variables or methods.
  
## Why is Class-Oriented Programming (COP) Bad? <a name="why-is-cop-bad"></a>
  - ###### why-is-cop-bad
  - The main problem with COP is that it's common practices lead to fragile code that was difficult to maintain and
    understand, for similar reasons as to why "Spaghetti Code" is difficult to maintain and understand.
  
  > The Pain of OOP, Lecture #3: Getters and naked data - Yegor Bugayenko
  > - https://www.youtube.com/watch?v=2YyVmIQQ23w

  > The Pain of OOP, Lecture #5: -ER Suffix is Evil - Yegor Bugayenko
  > - https://www.youtube.com/watch?v=6GMiosTLUTc 
  
  - Example of BOOP in Kotlin:
  
     ```mermaid
     flowchart LR
     
     subgraph Application
        subgraph Book
           subgraph Pages
              A("📄 Page 1 Content")-->|enclosed in| D
              B("📄 Page 2 Content") -->|enclosed in| D
              C("📄 Page 3 Content") -->|enclosed in| D
           end
            D("📑 List of Pages") -->|enclosed in| E(Book)
        end
        E("📖 Book") -->|enclosed in| F("🖥️ Application")
     end
     click F "https://github.com/realityexpander/How_to_program_from_ground_up/blob/main/src/main/kotlin/boopExample.kt" _blank
     
     ```
  - ### Back-to Object Oriented Programming Example (Kotlin): <a name="boop-example"></a>
  - ###### boop-example
    ```Kotlin
    class Page(  // <-- the Page class constructor
       private val content: String  // <-- the "val" keyword means the variable is immutable and can only be assigned once.
    ) {
      fun view() {
         println("Page: $content")
      }
      
      fun updateContent(newContent: String): Page {
         return Page(newContent)  // <-- the "updateContent" method is expected to return a new object with the new state.
      }
      
      fun inspectContent(): String {
         return content
      }
    }
  
    class Book(
       val title: String,
       private val pages: List<Page>
    ) {
       fun view() {
          println("Book: $title, # of Pages: ${pages.size}")
          pages.forEach { it.view() }
       }
       
       fun updateTitle(newTitle: String): Book {
          return Book(newTitle, pages)  // <-- The "updateTitle" method returns a new object with the new state.
       }
       
       fun updatePages(newPages: List<Page>): Book {
           return Book(title, newPages)  // <-- The "updatePages" method returns a new object with the new state.
       }
    }
  
    class Application(
       private val book: Book  // <-- The "Application" class, the "val" keyword means the variable is immutable.
    ) {
       fun view() {
          println("Application Viewing: ${book.title}")
          book.view()
       }
  
       fun updateBook(newBook: Book): Application {
          return Application(newBook)  // <-- The "updateBook" method returns a new object with the new state.
       }
    }
    
    // Start of Program
    fun main() {
       // Setup the App in the familiar Imperative Style:
       // Create the list of Page objects
       val pages = listOf(  // <-- the "val" keyword means the variable is immutable and can only be assigned once.
          Page("Page 1 Content"),
          Page("Page 2 Content"),
          Page("Page 3 Content")
       )
       // Create the book object using the list page objects
       val book = Book(
          "MyBook.txt",
          pages
       )
       // Create the application object using the book object 
       var app = Application(book) // <-- The "var" keyword means the variable is mutable,
                                   //     `app` is a "var" because it's expected to change state.
                                   // `app` is using the Singleton pattern, and it's allowed in BOOP, as its 
                                   // state is immutable.
    
       app.view()  // <-- will print:
                   // Application Viewing: MyBook.txtimp
                   // Book: MyBook.txt, # of Pages: 3
                   // Page: Page 1 Content
                   // Page: Page 2 Content
                   // Page: Page 3 Content
  
       // The above code could be arranged in the functional style, where the state of the program is created in 
       // a single line!
       //
       // - This style is also known as "declarative" style, as opposed to the familiar "imperative" style.
       // - Using declaritive style, the code is about "what" needs to be done, rather than step-by-step "how" to do it.
       // - As a programmer, you only see the high-level view, as the implementation details are hidden deeper 
       //   in the code, "abstracted" away in the functions.
       // - Functions are called and executed from the innermost brackets first to the outermost assignment last.
       // - The state of the program is created in a single call to the `Application` constructor.
       // - This style is also called "composition."
       
       // Setup the App in Functional Style:
       // The code executes from the innermost function to the outermost function (step 1 to step 5.)
       app = Application( // <-- Step 5 Creates a new Application object with the book object.
          Book( // <-- Step 4 Creates a new Book object with the
             title = "MyBook.txt",
             pages = listOf(  // <-- creates a new list of Page objects with the content "Page 1 Content", "Page 2 Content", "Page 3 Content"
                Page("Page 1 Content"), // <-- Step 1 Creates a new Page object with the content "Page 1 Content"
                Page("Page 2 Content"), // <-- Step 2 Creates a new Page object with the content "Page 2 Content"
                Page("Page 3 Content")  // <-- Step 3 Creates a new Page object with the content "Page 3 Content"
             )
          )
       )
  
       app.view()  // <-- will print the same as the imperative style:
                   // Application Viewing: MyBook.txtimp
                   // Book: MyBook.txt, # of Pages: 3
                   // Page: Page 1 Content
                   // Page: Page 2 Content
                   // Page: Page 3 Content
    
       ////////////////////////////////////////////   
       // Changing the State of the Application  //
       ////////////////////////////////////////////
      
       // app.book = Book("UpdatedBook.txt", emptyList())  // <-- will not compile, as the variable `book` is immutable
                                                           //     and cannot be modified. It can only be replaced.
       
       // To change the state of the application, a whole new object must be created with the new state,
       // usually based on a copy the old state, with modifications to reflect the new state.
       val newPages = pages
           .filter { page ->  // instead of using imperative "for" loops, "filter" internally uses a loop to create
                              // a new list of pages.
              page.inspectContent() != "Page 2 Content" // <-- removes the 2nd page from the list.
           }
           .toMutableList()  // <-- converts the immutable list to a mutable list to allow for adding a new page.
           .apply { // <-- creates a new list of pages with the same content as the original list, but with 
                    //     the 2nd page removed.
              add(  // <-- adds a new page to the list.
                 Page("New Page 4 Content")  // <-- creates a new page with the content "New Page 4 Content"
              )
           }
           .toList()  // <-- converts the mutable list back to an immutable list.
       
       // The `updateBook` method is called to update the `book` which will create a `app` with the new state.
       app = app.updateBook(
          app.book // <-- Using the `book` from the current state of the application to copy the state of the `book`.
             .updateTitle("UpdatedBook.txt") // <-- Creates a new book with the updated name and the same `pages`.
             .updatePages(newPages)  // <-- Creates a new book with the updated `pages` and the same `title`.
       )
       
       app.view()  // <-- will print:
                   // Application Viewing: UpdatedBook.txt
                   // Book: UpdatedBook.txt, # of Pages: 3
                   // Page: Page 1 Content
                   // Page: Page 3 Content
                   // Page: New Page 4 Content
    }
    
    main()
  
    // Output:
    // Application Viewing: MyBook.txt
    // Book: MyDocument.txt, # of Pages: 3
    // Page: Page 1 Content
    // Page: Page 2 Content
    // Page: Page 3 Content
    // Application Viewing: UpdatedBook.txt
    // Book: UpdatedBook.txt, # of Pages: 3
    // Page: Page 1 Content
    // Page: Page 3 Content
    // Page: New Page 4 Content
    
    ```
    > Live Code Example: [BOOP example](src/main/kotlin/boopExample.kt)   

- [Continue Reading - Functional Programming](./11-FunctionalProgramming.md)
- [Back to Index](README.md)