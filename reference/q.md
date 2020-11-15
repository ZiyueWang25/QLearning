# q

1. Operation Lists
   1. 0 +/ 10 20 30 40 50
   2. (+/) 10 20 30 40 50
   3. (*/) 1 2 3 4 5
   4. (*/) 1 + til5
   5. (*/) 1 + til10
   6. 4 | 5 / take the larger one, 5
   7. 10 | 2 
   8. 10 & 2 / take the smaller one
   9. (|/) 10 30 20 50 40 / maximum of the list
   10. (&/) 10 30 20 50 40 / minimum of the list
   11.  / sum min max
   12. 0b|1b / or
   13. 0b&1b / and 
   14. (+\ ) 10 20 30 40 50 / keep the intermediate result, running sum  sums
   15. (&\ ) / running minimum  mins
   16. (|\ ) / runnning maximum  maxs

2. Defining Functions
   1. {[x]x*x} / square
   2. {[x]x*x}5  / get 25
   3. {x*x}5 / implicit function, no way easier
3. Functional Examples
   1. newton raphson {[xn] xn + (2-xn * xn) % 2 * x}/[1.0] / calculate until 10^{-14} precision
   2. \P 16 / adjust precision to 16 places
   3. 2#10 20 30 40 50 / retrive number of elements from the list
   4. 10 20, 100 200 300 / “,” for join operator
   5. {x, sum -2#x} 1 1 / fibonacci
   6. {x, sum -2#x}/ [10; 1 1] / fibonacci 10 times
4. Functions Example: Variable
   1. deltas 10 20 30 40 50 : 10 10 10 10 10
   2. deltas 110 120 130 140 150: 110 10 10 10 10
   3. deltas sums 1 2 3 4 5: sums deltas 1 2 3 4 5
   4. a:42
   5. buys: 2 1 4 3 5 4
   6. sell: 12
   7. deltas sell & sums buys / allocation
5. Table
   1. collections of columns
   2. dates:2018.01.01 + til 1000000?31
   3. times: 1000000?24:00:00.0000
   4. qtys: 100*1 + 1000000?100
   5. ixs:1000000?3
   6. syms:`aapl  `amzn `goog ixs /list can be a function
   7. pxs: (1000000?0.03)* 172.0 01189.0 1073.0 isx 
   8. t:([] date:dates; time:times:sum: syms;qty:qtys; px:pxs)
   9. t: \`date `time xasc t
   10. 5#t
6. qSOL
   1. select date, time, qty, px from t where sym=`aapl
   2. \t … \how mny ms it takes
   3. first 10 20 30 40 50
   4. last 10 20 30 40 50
   5. 5#select open:first px, close: last pxs, lo: min px, hi: max px by date, time from t where sym=`aapl
7. complex queries
   1. weigthed average function
      1. 4 3 2 1wavg 10 20 30 40
   2. 5 xbar 0 1 2 3 4 5 10 11 21 \ 0 0 0 0 0 5 10 10 20
   3. select max px - mins px from t where sym=`aapl

8. Interprocess Communication
   1. server and client
   2. server:
      1. open a port: \p 4242 \open a server id with 4242
      2. cub3:{x * x * x}
      3. cub3:{ON!x * x * x} : show the result and pass to the next
   3. client:
      1. h:hopen `::4242 \open the collection
      2. h “6*7” \ remote server compute it
      3. sq:{x*x}
      4. h (sq; 5)
      5. h (`cub3; 5)
9. Callbacks
   1. server
      1. cub3: {ON!.z.w x * x * x}
      2. worker:{[arg; callback] r:cub3 arg; (neg .z.w) (callback; r)}
   2. client
      1. h  \ it is 3i, use the integer as a function
      2. (neg h) (`cub3; 5) \ async call
      3. continue:{ON! x}\ call back
      4. (neg h) (\`worker; 5;  `continue)
10. I/O 
    1. string is a list of character
       1. count “jab” / list of string, return 3
       2. count `jab / it is a item so it returns 1
    2. file I/O
       1. (“So long”; “and thanks”; “for all the fish”) / general notation for list () with ; as separator
       2. `:/data/solong.txt 0: (“So long”; “and thanks”; “for all the fish”)
       3. \`:/data/answer.txt 0: txt, txt: read0 `:/data/solong.txt

