# Testing

This week we were provided with a new repository by our module leader which was for a "Hangman" game. The objective of providing this repository
was to run test battles. The code for the game would run but there were functions we had to complete, and then had to create unit tests for those function
using Xunit framework. 

## Unit Test

The code I tested was for 'CheckLetterInWord' function which was a part of the Hangman game. This function is responsible for checking weather a user entered
letter is a part of the word they are guessing based on the game type i.e. easy, medium and hard. Its purpose is to accurately check the letters in the word for
the Hangman game. 

### Test Code


<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/unittest1.png" width="300" height="200">
<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/unittest2.png" width="300" height="200">
<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/unittest3.png" width="300" height="200">
<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/unittest4.png" width="300" height="200">

### Explanation 

1. Test_CheckLetterInWord_Easy_True: Tests if the CheckLetterInWord function is correctly returning true for letter 'a' which is in the easy difficulty word "aadi",

2. Test_CheckLetterInWord_Easy_False: Tests if the function is correctly returning false for letter 'z' that is not present in the easy difficulty word "aadi",

3. Test_CheckLetterInWord_Medium_True: Tests if the function is correctly returning true for letter 'a' which is in the medium difficulty word "adarshaa",

4. Test_CheckLetterInWord_Medium_False: Tests if the function is correctly returning false for letter 'z' that is not present in the medium difficulty word "adarshaa",

5. Test_CheckLetterInWord_Hard_True: Tests if the function is correctly returning true for letter 'o' which is in the hard difficulty word "mounteverest",

6. Test_CheckLetterInWord_Hard_False: Tests if the function is correctly returning false for letter 'l' that is not present in the hard difficulty word "mounteverest",

These tests are essential as they are verifying the correctness of vital functionality of the hangman game which is checking a given word is a part of the word which is being guessed.
This is an important part of the game and is necessary to get it right to avoid any issues in the games experience. 

The test only focuses on the individual letter checking part of the functionality and don't cover other aspects of the game which is what its limited to. 
