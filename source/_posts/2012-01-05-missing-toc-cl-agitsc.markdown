---
layout: post
title: "The Missing Table of Contents of Common Lisp - A Gentle Introduction to Symbolic Computation"
date: 2012-01-05 23:25
comments: true
categories: ["Common Lisp"]
tags: lisp
published: true
---

I thought this book does not have table of contents first...
So I compiled this list, then I found it's at the end of the book..

Holy crap......I am such an idiot!!!!!

<!--more-->

Preface    
Note to Instructors       
Acknowledgements

1. Functions and Datas    
1.1. Introduction    
1.2. Functions on Numbers    
1.3. Three Kinds Of Numbers    
1.4. Order of Input Is Important    
1.5. Symbols    
1.6. The Speical Symbols T and NIL    
1.7. Some Simple Predicates    
1.8. The Equal Predicate    
1.9. Putting Functions Together    
1.10. The NOT Predicate    
1.11. Negating a Predicate    
1.12. Number of Inputs to a Function    
1.13. Errors    
1 Advanced Topics    
1.14 The History of Lisp    

2. Lists    
2.1. Lists are the most versatile Data Type    
2.2. What do Lists look like    
2.3. Lists of one Element    
2.4. Nested Lists    
2.5. Length of Lists    
2.6. NIL: The Empty List    
2.7. Equality of Lists    
2.8. First, Second, Third, AND REST    
2.9. Functions Operate on Pointers    
2.10. CAR and CDR    
2.11. CONS    
2.12. Symmetry of CONS and CAR/CDR    
2.13. LIST    
2.14. Replacing the first element of a list    
2.15. LIST Predicates    
2 Advanced Topics    
2.16. Unary Arithmetic with Lists    
2.17. Nonlist Cons Structures    
2.18. Circular Lists    
2.19. Length of Nonlist Cons Structures    

3. EVAL Notation    
3.1. Introduction    
3.2. The EVAL Function    
3.3. Eval Notation can do anything box notation can do    
3.4. Evaluation rules define the behavior of EVAL    
3.5. Defining Functions in EVAL notation    
3.6. Variables    
3.7. Evaluating Symbols    
3.8. Using Symbols and Lists as Data    
3.9. The problem of misquoting    
3.10. Three ways to make lists    
3.11. Four ways to misdefine a function    
3.12. More about variables    
LISP on the Computer        
3.13. Running LISP    
3.14. The READ-EVAL-PRINT Loop    
3.15. Recovering From Errors    
LISP Toolkit: ED        
Keyboard Exercise    
3 Advanced Topics    
3.17. The quote special function    
3.18. Internal Structure of Symbols    
3.19. Lambda notation    
3.20. Scope of Variables    
3.21. EVAL and APPLY    

4. Conditionals      
4.1. Introduction    
4.2. The IF Special Function    
4.3. The COND Marcro    
4.4. Using T as a Test    
4.5. Two More Examples Of COND    
4.6. COND and Parenthesis Errors    
4.7. The AND and OR Macros    
4.8. Evaluating AND and OR    
4.9. Building Complex Predicates    
4.10. Why AND and OR are Conditionals    
4.11. Conditionals Are Interchangeable    
Lisp Toolkit: STEP    
4 Advanced Topics    
4.12. Boolean Functions    
4.13. TRUTH tables    
4.14. Demorgan's Theorem    

5. Variables and Side Effects    
5.1. Introduction    
5.2. Local and Global Variables    
5.3. SETF assigns a value to a variable    
5.4. Side Effects    
5.5. The LET Special Function    
5.6. The LET* Speical Function    
5.7. Side Effects can Cause BUGS    
Lisp Toolkit: DOCUMENTATION and APROPOS    
Keyboard Exercise     
5 Advanced Topics       
5.8. Symbols and Value Cells    
5.9. Distinguishing Local from Global Variables    
5.10. Binding, Scoping, and Assignment    

6. List Data Structure    
6.1. Introduction    
6.2. Parenthesis Notation VS. CONS cell notation    
6.3. The APPEND Function    
6.4. Comparing CONS, LIST, AND APPEND    
6.5. More Functions on Lists    
6.5.1. REVERSE    
6.5.2. NTH and NTHCDR    
6.5.3. LAST    
6.5.4. REMOVE    
6.6. LISTS AS SETS    
6.6.1. MEMBER    
6.6.2. INTERSECTION    
6.6.3. UNION    
6.6.4. SET-DIFFERENCE    
6.6.5. SUBSETP    
6.7. Programming with SETs    
6.8. LISTs as TABLEs    
6.8.1. ASSOC    
6.8.2. RASSOC    
6.9. Programming with TABLEs    
Lisp Toolkit: SDraw    
Keyboard Exercise         
6 Advanced Topics     
6.10. TREEs    
6.10.1. SUBST    
6.10.2. SUBLIS    
6.11. Efficiency of LIST operations    
6.12. Shared Structure    
6.13. Equality of Objects    
6.14. Keyword Arguments    

7. Applicative Programming    
7.1. Introduction     
7.2. FUNCALL    
7.3. The MAPCAR operator    
7.4. Manipulating TABLEs with MAPCAR    
7.5. LAMBDA Expression    
7.6. The FIND-IF operator    
7.7. Writing ASSOC with FIND-IF    
7.8. REMOVE-IF AND REMOVE-IF-NOT    
7.9. The REDUCE operator    
7.10. EVERY    
Lisp Toolkit: TRACE and DTRACE    
Keyboard Exercise         
7 Advanced Topics     
7.11. Operating on Multiple LISTs    
7.12. The Function Special Function    
7.13. Keyword Arguments to Applicative Operators    
7.14. Scoping and Lexical Closures    
7.15. Writing and Applicative Operator    
7.16. Functions that Make Functions    

8. Recursion    
8.1. Introduction         
8.2. Martin and The Dragon    
8.3. A Function to search for odd numbers    
8.4. Martin VISITS The Dragon AGAIN    
8.5. A LISP version of the Factorial Function    
8.6. The Dragon's Dream    
8.7. A Recursive Function for counting slices of bread    
8.8. The Three Rules of Recursion    
8.9. Martin Discovers Infinite Recursion    
8.10. Infinite Recursion in LISP    
8.11. Recursion Templates    
8.11.1. Double-Test Tail Recursion    
8.11.2. Single-Test Tail Recursion    
8.11.3. Argumenting Recursion    
8.12. Variations on the basic templates    
8.12.1. List-Consing Recursion    
8.12.2. Simultaneous Recursion on Several Variables    
8.12.3. Conditional Argumentation    
8.12.4. Multiple Recursion    
8.13. TREEs and CAR/CDR Recursion    
8.14. Using Helping Functions    
8.15. Recursion in ART and LITERATURE    
Keyboard Exercise             
Lisp Toolkit: The Debugger        
8 Advanced Topics       
8.16. Advantages of tail recursion        
8.17. Writing new Applicative Operators        
8.18. The Labels Special Function    
8.19. Recursive Data Structures        

9. Input/Output    
9.1. Introduction    
9.2. Character Strings    
9.3. The FORMAT Function    
9.4. The READ Function    
9.5. The YES-OR-NO-P Function    
9.6. Reading FILES with WITH-OPEN-FILE    
9.7. Writing FILES with WITH-OPEN-FILE    
Keyboard Exercise         
Lisp Toolkit: DRIBBLE        
9 Advanced Topics       
9.8. Parameters to FORMAT Directives      
9.9. Additional FORMAT Directives      
9.10. The LISP 1.5 OUTPUT Primitive      
9.11. Handling END-OF-FILE Conditions      
9.12. Printing in DOT notation      
9.13. Hybrid notation      

10. Assignment      
10.1. Introduction      
10.2. Updating a Global Variable      
10.3. Stereotypical Updating Methods      
10.3.1. The INCF and DECF Macros      
10.3.2. The PUSH and POP Macros      
10.3.3. Updating Local Variables      
10.4 WHEN and UNLESS      
10.5. Generalized Variables      
10.6. Case study: A TIC-TAC-TOE Player      
Lisp Toolkit: BREAK and ERROR       
10 Advanced Topics         
10.7. DO-IT-YOURSELF LIST surgery      
10.8. Destructive Operations On LISTs      
10.8.1. NCONC          
10.8.2. NSUBST      
10.9. Programming with Destructive Operations      
10.10. SETQ and SET      

11. Iteration and Block Structure      
11.1. Introduction    
11.2. DOTIMES and DOLIST    
11.3. Exiting the body of a LOOP    
11.4. Comparing Recursive and Iterative search    
11.5. Building up results with assignment    
11.6. Comparing DOLIST with MAPCAR and Recursion    
11.7. The DO Macro    
11.8. Advantages of implicit assignment    
11.9. The DO* Macro    
11.10. Infinite loops with DO    
11.11. Implicit Blocks    
Keyboard Exercise         
Lisp Toolkit: TIME    
11 Advanced Topics    
11.12. PROG1, PROG2 and PROGN    
11.13. OPTIONAL arguments    
11.14. REST arguments    
11.15. Keyword arguments    
11.16. Auxiliary Variables    

12. Structures and The Type System    
12.1. Introduction    
12.2. TYPEP and TYPE-OF    
12.3. Defining Structures    
12.4. Type predicates for structures    
12.5. Accessing and Modifying Structures    
12.6. Keyword arguments to Constructor Functions    
12.7. Changing Structure Definitions    
Lisp Toolkit: DESCRIBE and INSPECT    
Keyboard Exercise     
12 Advanced Topics    
12.8. PRINT functions for Structures    
12.9. Equality of Structures    
12.10. Inheritance from other structures    

13. Arrays, Hash Tables, And Property Lists    
13.1. Introduction    
13.2. Creating an Array    
13.3. Printing Arrays    
13.4. Accessing and Modifying Array Elements    
13.5. Creating Arrays with MAKE-ARRAY    
13.6. Strings as Vectors    
13.7. Hash Tables    
13.8. Property Lists    
13.9. Programming with Property Lists    
Array Keyboard Exercise    
Hash Table Keyboard Exercise    
Lisp Toolkit: ROOM    
13 Advanced Topics    
13.10. Property List Cells    
13.11. More on Sequences    

14. Macros and Compliation    
14.1. Introduction    
14.2. Macros as shorthand    
14.3. Macro Expansion    
14.4. Defining a Macro    
14.5. Macros as syntactic extensions    
14.6. The backquote character    
14.7. Splicing with backquote    
14.8. The compiler    
14.9. Compliation and Macro expansion    
14.10. Compiling entire programs    
14.11. Case study: Finite State Machines    
Lisp Toolkit: PPMX    
Keyboard Exercise    
14 Advanced Topics    
14.12. The &BODY LAMBDA-LIST keyword    
14.13. Destructuring Lambda Lists    
14.14. Macros and Lexical scoping    
14.15. Historical Significance of Macros    
14.16. Dynamic Scoping    
14.17. DEFVAR, DEFPARAMETER, DEFCONSTANT    
14.18. Rebinding special variables    

Appendix A The SDRAW Tool    
Appendix B The DTRACE Tool    
Appendix C Answers to Exercises    
Glossary    
Index    
Contents    
