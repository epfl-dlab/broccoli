# Data
This repository contains data collected in our user study on the efficiency of the Broccoli paradigm.\
For a detailed evaluation please refer to: <enter paper URL here>

A detailed schematic of the data is recorded in the following

## Data from first session
`german_learning.json` and `swiss_learning.json` contain data collected by our plugin during the first session.
In this session, participants were exposed to two tables of vocabulary and a selection of annotated text.
The JSON files contain lists, each entry corresponds to a participant.\
Each entry in the list is a dictionary of relevant userdata. The keys found in the entry are:
 - `userDataReference`: Under this key, the plugin has stored the users' email. It has been replaced by an integer that uniquely identifies this user.
 - `popups`: Everytime the user clicks on a word during the annotated reading section, a popup with its translation is shown on screen.
     - `lemma`, the word that was translated
     - `timestamp`, the time at which the popup was created
 - `readingTimestamps`: Each time the user enters or leaves a page during the annotated reading section, the plugin creates a readingTimestamp.
    The number of words shown to the user, both annotated and unannotated, can be found in lemma_counts.json.
    By combining timestamp data and word counts you can compute a reading speed in words-per-minute
     - `direction`, in ['enter', 'exit']. Encodes whether the user entered or left the page.
     - `timestamp`, the time when this event occured.
     - `currentIndex`, the number of the site that was page
     - `html_displayed`, the content of the site. If no `<mark>` html tags are present, the text doesn't contain Broccoli annotations.
 - `readingSpeedData`: For the second deployment, the plugin was refined to be more self-contained. This key is only present in the data collected in Germany.
    It contains both the time spent reading and the number of words read.
     - `total_time_annotated`, total amount of time spent reading text with annotations
     - `total_time_vanilla`, total amount of time spent reading unprocessed text
     - `lemmas_with_annotations`, number of words in annotated text
     - `lemmas_without_annotations`, number of words in unannotated text
 - `ressources`: The words assigned to the different conditions are recorded here. To identify which group a user belongs to, you should rely on the wordgroups recorded in this first session. The long-term followup in Switzerland has been done remotely, we couldn't verify whether participants install the right plugin. For security, we check against the words recorded under this `ressources` key. Users can be identified uniquely by their id.
    - `a` words shown in the pre-table condition.
    - `be` and `br` are "Broccoli with language model" and "Broccoli at random", respectively.
    - `c` words shown in the post-table condition. 
 - `testAnswers`: A list with answers from the multiple choice test. Each entry contains
     -  `choices`, a list of answer options.
     -  `given`, the word to be translated
     -  `correct`, the correct translation
     -  `selected`, a one-hot encoding of the participants answer
     - `unknown`, a boolean indicating whether the participant selected 'unknown' as the answer
     -  `word_group`, the condition in which this word was learned, the value is in ['a', 'be', 'br', 'c']
     - `timestamp`, the time at which the question was answered

## Data from second session
The german_followup.json and swiss_followup.json files contain results from the followup test.
This test consisted only of a vocabulary test. No reading data has been created. Apart from that, the data has the same layout as for the first session of the study.

## Fill-the-gap
The answers in the fill-the-gap section have been gradedd manually.
Data can be found in `fill_the_gap_rated.csv`, answers have been encoded as follows:
 - -1, this word was not asked in the test
 - "" or " ", this gap was not filled by the user
 - 0, the answer was false
 - 1, the answer was correct
 - 2, the given answer was a synonym to the correct answer.

## Survey Data
Before and after the first session of the study, as well as after the second session, we have asked our participants to fill in Forms.
Among others, the questions that have been asked where:
 - their age/gender/education
 - their native language(s)
 - languages they know
 - their interactions with the study
 - their experience

The data can be found in `before_survey.csv`, `after_survey.csv` and `after_followup.csv`.
It should be compatible with common spreadsheet software.
One column contains the participants email. It has been replaced with a uniquely identifying integer. This is the same ID as in the JSON files described above.
# Prototype
As part of our research on Broccoli, we have created a prototype of our learning tool.\
It is intended as a reference and platform for further research.\
The code can be found here: https://github.com/epfl-dlab/broccoli-plugin