This is Alexander Sharpe's report for Project 1 of Large Scale Data Processing. All executions of the program use a singular Eagle ID as the bitcoin block: 27964563.

# Part 1

## k=2: 
- xS = 13174709327964563
- Hash = 008956a714f67e6804de26bda031d53bc0774aa498f228975d5b28dc069b6436
- Time Elapsed = 1s 
- Num Trials = 331

## k=3:
- xS = 28168362527964563
- Hash = 0002c8a8f5db4e52961310b0e2544385e684524b7405145afb62b792ed58c0d9
- Time Elapsed = 1s
- Num Trials = 1823
  
## k=4:
- xS = 20713561727964563
- Hash = 00003eb86d08c400abe5d811958a7ccd7a79e9f8bb07a96e53201d9be09487cb
- Time Elapsed = 1s
- Num Trials = 44671

## k=5:
- xS = 178489599427964563
- Hash = 00000e105b4480bb5da9ab38645b4d9b960f2d8cd290840bae49f81b877051aa
- Time Elapsed = 4s
- Num Trials = 889100

## k=6:
- xS = 96015056427964563
- Hash = 000000134a4a1f39d9595deee021c890d463c801f052dfa1d6d1b6ce44aedd0e
- Time Elapsed = 32s
- Num Trials = 36089532

# Part 2

## k=7:
- xS = 160722198027964563
- Hash = 0000000e04e04767c764f56ed74cd7618a908a1b38e4f32e1934bd370fe9c159
- Time Elapsed = 964s
- Num Trials = 194163338

  The cluster has 4 HDFS Data Nodes, of which the Metrics Explorer says 3.07 were running during job operations. Within each of the nodes, there were 7.86 YARN virtual cores. In order to find the number of trials that needed to find the nonce, I modified the code slightly: I added a counter, which only counted the number of trials up until the correct answer was found, whereas previously, the code would just complete num_trials trials even if the correct answer was found earlier (it just stored all results and then found the correct one after). These edits can be found in src/main/scala/project_1/main.scala.

# Part 3

  I replaced the line for nonce generation with: val nonce = sc.range(1, trials + 1). Efficiency advantages of this sequential generation are: 
  
  - Ensures that all possible nonces in the given range are checked
  - No risk of repeating numbers
  - Some partitions may have duplicate numbers in the random approach
  - If a valid nonce exists in the range, it will be found, whereas random could miss valid nonces

  Some efficiency disadvantages are:

  - Slower if the solution is near the end of the range
  - Very slow for large search spaces

  This approach is more efficient in certain cases, mainly when the range for our nonce is small, otherwise it could become very inefficent. 

  
