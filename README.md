

# NER TASK

This repo contain the code to extract the speaker name from  each utterance in the  transcript. 

## Installation of Library

The python libraries pandas and spaCy is used in this code. 

```python
import pandas as pd
import spacy
from spacy import displacy
filename='---' #name of file containing transcript
```



##  Approach

1) Using `NER` function of `SpaCy` library, name/Entity were extracted from utterances.

2. Only Person/Speaker names from name/Entity list were extracted.

3. From speaker list, identified speaker is replaced with  name .

4. If the Utterance has single name of speaker , then that name will be the identified speaker.

5. If the Utterance has more than one speaker identified, then we implement following logic given below

   ````text
   if dialgoue contain names >1:
      if name not assigned above to any speaker and given utterance has not been assigned speaker name yet:
      		assign name to speaker and add the name to assigned list
      	
      		
   ````

6. If the tie is created in above condition, first name is selected for speaker name.

   ## Limitation of Approach

   The applied approach use rule-based system to give name to speaker. It work on given `transcript` file but could face problems in unseen transcript because of following assumptions

   1. Speaker first introduce him/her so first name should be a speaker name

   2. If someone calls the other person name first  then called named person should introduce himself before this person call.

   3. Normally, in introductory utterance person introduce himself. So, first name is speaker name but if someone call other person name before his name in its utterance like in third utterance of  `transcript` file. The third Utterance shown

      ````` text 
      Speaker3: Thanks David. So as David said, I’m Sally, Sally Jones, I’ve been in book sales for 10 years now.
      `````

      In above, the speaker first thanks David then introduce himself. Taking first name here is getting wrong speaker name but David is already taken in second utterance as speaker. So , David selection for this utterance speaker is avoided because he is assigned to some utterance before.

      

      Usually during conversation if someone is asked to introduce himself/herself then most probably the first name he/she speak is his/her name. If he/she speaks other persons name then high probability is that person already introduce himself and you have that name to the speaker list above. If unseen transcript contain utterances that have some other way to introduction speaker, then the given code will not work accurately. In linguistic, we cannot limit the way of introducing  so generic rule were implemented in this code to capture most of the utterances.