Download Link: https://assignmentchef.com/product/solved-csci862-system-security-assignment-1
<br>
<h1>Part One: Short answer questions:                                                      4 Marks</h1>

<ol>

 <li>A phonetic segment generator works as follows. Each segment has 3 English letters. The form ofeach segment is ∆Φ∆ (consonant, vowel, consonant), where Φ is an element in {a, e, i, o, u} and ∆ is an English letter which is not in {a, e, i, o, u}. Determine the entropy associated with the following method of generating a password. <strong>1 Mark</strong></li>

</ol>

Choose, and place in this order, one phonetic segment cosisting of lower case letters, followed by three digits and then two symbols drawn from the set {+,*,@,#,$}. Finally, apply Whirlpool to give an output string in hex which will be used as a password.

You should assume the random choices are made with equal likelihood of each symbol from the space being chosen. So for a random digit there are 10 possibilities each of which is chosen with probability 1/10.

<ol start="2">

 <li>Consider the following statements and answer the subsequent questions:</li>

</ol>

Alice can climb walls and jump fences.

Bob can push walls and push doors.

Chris can push Alice, push fences and jump walls. Dan can open doors and jump Alice.

<table width="673">

 <tbody>

  <tr>

   <td width="593">(a) What are the subjects, objects and actions for this scenario?</td>

   <td width="80"><strong>0.25 Mark</strong></td>

  </tr>

  <tr>

   <td width="593">(b) Draw an access control matrix representing this scenario.</td>

   <td width="80"><strong>0.25 Mark</strong></td>

  </tr>

 </tbody>

</table>

<ol start="3">

 <li>Consider the lattices in the file A1-Q3.pdf and answer the questions below. A line going down from level <em>X </em>to level <em>Y </em>indicates that level <em>X </em>dominates level <em>Y </em>. Assume this diagram is with reference to BLP. For the questions other than the first you can work with whichever of the diagrams you feel most comfortable with. Justify your answers.

  <ul>

   <li>How are the diagrams A and B related as lattices? <strong>25 Mark</strong></li>

   <li>I have one object at level 1010 and another object at 0001. What is the most appropriate levelfor a subject to be assigned so both objects can be read by the subject? <strong>25 Mark</strong></li>

   <li>I have one subject at level 0110 and another subject at 0111. What is the most appropriatelevel for an object to be assigned so both subjects can append to the object? <strong>25 Mark</strong></li>

   <li>I have three objects, one at 1000, one at 0100, and one at 0010. What is the most appropriatelevel for a subject to be assigned so all three objects can be read by the subject? <strong>25 Mark</strong></li>

   <li>Explain how the digits can be interpreted in a multilateral and multilevel sense. <strong>5 Mark</strong></li>

  </ul></li>

 <li>Assume that Alice has registered with the server Bob to use Lamport’s one–time password scheme.Alice’s password is Alice1234567, where you should replace the 1234567 with your own student number. If <em>n </em>= 10 initially, what are the first two and the last one–time passwords transmitted by</li>

</ol>

Alice? Use MD5 as the hash function.                                                                                       <strong>0.5 Mark</strong>

<ol start="5">

 <li>Consider the BLP level relationship diagram in 862-A1-Q5.pdf, and the associated explanation ofthe notation, and answer the subsequent questions.

  <ul>

   <li>Does the diagram define a lattice? Justify your answer. <strong>25 Mark</strong></li>

   <li>Assume that if the diagram didn’t define a lattice you have fixed it so it does, without changingthe relationships between the existing levels. Some of the domination relationships shown in the diagram are redundant. Identify two such lines and explain why they are unnecessary.</li>

  </ul></li>

</ol>

<strong>0.25 Mark</strong>

<h1>Part Two: Implementing a rainbow table                                        8 Marks</h1>

You are to write a program, in C/C++ or Java, that compiles on Banshee with an instruction you provide. It should run on Banshee using the following instruction:

$ ./Rainbow Passwords.txt

where the file Passwords.txt contains a list of possible passwords. The password file contains a password per line, as in /usr/dict/words and consists of strings of printable characters. Any password used must be taken from this file, so the only stored hash information needs to relate to those entries in the file.

The program is used to find pre–images for given hash values. Rainbow tables can be used to solve pre–image problems for hash functions. At the simplest level they can simply be a list of hash values and the corresponding pre-images, often from some dictionary. This can be expensive in terms of storage space however, and a more efficient way of identifying pre-images involves the use of the hash function and reduction functions.

Your program will do some initial computations to generate the rainbow table. The process is as follows:

<ol>

 <li>Read in the list of possible passwords.</li>

 <li>For each previously unused word <em>W</em>, first mark it as used and then carry out the following process:

  <ul>

   <li>Apply the hash function <em>H </em>to the word <em>W </em>to produce a hash value <em>H</em>(<em>W</em>), which we refer to as the current hash.</li>

   <li>Apply the reduction function <em>R </em>to the current hash, which will give a different possible password which should be marked as used and then hashed. The resulting hash value is recorded as the current hash.</li>

   <li>Repeat the previous step four times. You can deal with collisions if you like but are not requiredto.</li>

   <li>Store the original word <em>W </em>and the final current hash as an entry in your rainbow table.</li>

  </ul></li>

 <li>To assist with the later identification of the pre–images you should sort the rainbow table based onthe hash values.</li>

 <li>Output the list of words and corresponding “final current hashes” to a text file txt.</li>

</ol>

You are now ready to carry out the second part of the exercise, finding pre-images. Request a hash value from the user. There should be appropriate error checking as to the length of the input string etc. The process of identifying the pre–image for the provided hash value is sketched as follows:

<ol>

 <li>Check if the hash value is in the rainbow table.</li>

 <li>If the hash value isn’t in the rainbow table you hash and reduce until you get a hash value that is inthe rainbow table, or until you have done the hash and reduce enough times that it’s clear from the way the rainbow table is generated that something is wrong. Display an appropriate message if this happens.</li>

 <li>Once you have identifed the relevant hash value in the table you take the corresponding passwordand hash it. If that is your hash value you have your pre–image. If it isn’t, then reduce and hash again, until the reduced word hashes to the hash value being searched for.</li>

 <li>Output the releative reduced word, that is your pre–image.</li>

</ol>

A reduction function is designed to take a valid hash value and return a valid word, in this case a valid word from Passwords.txt. The reduction function to be used is based on the number of words in the Passwords.txt file. You should take an appropriate number of bits from the front of the hash function, convert that to an integer that identifies one of the passwords. You should use MD5 as the hash function.


