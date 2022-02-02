# Wordler

Wordler takes two or more command line parameters and suggests words you might use to solve the puzzle.
I don't endorse the use of this tool, or anything like it.

# Warning
You can decide for yourself if this is a cheat or something else, but this will take the fun out of Wordle.

## Install
this is just a small shell script. 

1. put it on your computer
2. adjust the path to point to your [dictionary file](https://github.com/bnprks/wordle_solver/blob/master/answers.txt)
3. make it executable

## Usage

1. To get started, guess a word and see what you get as a result.
2. Encode your result from the prior guess into the command line.
3. Select your next guess from the proposals offered by Wordler.
4. Repeat until you solve the puzzle for the day.

## Encoding your result

Invoke the tool from the command line. The parameters take the following form:

```wordler <pattern> <letters not in word> [yellow] [yellow] [...]``` 

Parameters:
`pattern`: a regular expression, usually needs to be "quoted" to work in your shell. This commonly takes one of three forms:

  1. a green letter just appears in the correct position
  2. a yellow letter is represented using NOT logic indicating where it cannot appear in the solution
  3. a placeholder for any positions for which nothing is known

`letters not in word`: any letters you have guessed but which are not found in the solution today

`yellow`: [OPTIONAL] each letter which appears in the solution but for which the position is currently unknown 

### Example

#### Step 1
Imagine you use `wreck` as your first guess. The `r` shows as green.

This would be encoded as:
  `wordler ".r..." weck`

The <pattern> parameter indicates: 
- you know the second position is an R
- you have no clues about the value for the other positions

The <letters not in word> parameter indicates that none of W E C or K appear in the solution

Wordler will recommend some options  
  
#### Step 2
Imagine you use `frame` as your second guess. The `r` shows as green and the `a` shows as yellow.

This would be encoded as:
  `wordler ".r[^a].." weckfm a`

The <pattern> parameter indicates: 
- you know the second position is an R
- you know that the third position is NOT an A (here this is expressed as `[^a]` but you can use any regular expression) 
- you have no clues about the value for the remaining positions

The <letters not in word> parameter indicates:
- the letter F does NOT appear in the solution
- the letter M does NOT appear in the solution
- the letter E does NOT appear in the solution
  
Optionally: add additional parameters, one for each letter which you know appears in the solution, but which you don't have a position for. 
In this case that is just the single A here.

