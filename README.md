Textanalyse in R: eine Einführung
================
Johannes B. Gruber

# Introduction

The availability of text data has exploded in the last two decades.
First the availability of text through digital archives, then the advent
of digital media communication like online news and press releases and
most recently public communication of non-elite actors on social media.
For political science this opens up exciting new possibilities for
research as many processes which occurred in private or elite venues is
now accessible. At the same time, the sheer amount of data makes
manually analysing meaningul fractions of it impossible.

This course is an introduction to the available methods and software for
automated content analysis. The 101 in it’s name is meant to indicate
that this is a introductory course. However, the introductory part is
into automated content analysis while the expectation is that you are
comfortable with R, the programming language used in this course.

What should be clear about the course from the beginning though is that
despite recent advances, “All Quantitative Models of Language Are
Wrong—But Some Are Useful” (Grimmer and Stewart 2013, 3). The primary
goal of this course is thus to understand the types of questions we can
ask with text, and how to go about answering them.

In this two-day course, we are going to look at the different topics
mostly from a practical standpoint with a little theoretical and
statistical background where necessary. The schedule looks as follows:

<div id="vepjlbijat" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#vepjlbijat .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#vepjlbijat .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#vepjlbijat .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#vepjlbijat .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#vepjlbijat .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 0;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#vepjlbijat .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vepjlbijat .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#vepjlbijat .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#vepjlbijat .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#vepjlbijat .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#vepjlbijat .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#vepjlbijat .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#vepjlbijat .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#vepjlbijat .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#vepjlbijat .gt_from_md > :first-child {
  margin-top: 0;
}

#vepjlbijat .gt_from_md > :last-child {
  margin-bottom: 0;
}

#vepjlbijat .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#vepjlbijat .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#vepjlbijat .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#vepjlbijat .gt_row_group_first td {
  border-top-width: 2px;
}

#vepjlbijat .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#vepjlbijat .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#vepjlbijat .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#vepjlbijat .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vepjlbijat .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#vepjlbijat .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#vepjlbijat .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#vepjlbijat .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#vepjlbijat .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#vepjlbijat .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-left: 4px;
  padding-right: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#vepjlbijat .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#vepjlbijat .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#vepjlbijat .gt_left {
  text-align: left;
}

#vepjlbijat .gt_center {
  text-align: center;
}

#vepjlbijat .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#vepjlbijat .gt_font_normal {
  font-weight: normal;
}

#vepjlbijat .gt_font_bold {
  font-weight: bold;
}

#vepjlbijat .gt_font_italic {
  font-style: italic;
}

#vepjlbijat .gt_super {
  font-size: 65%;
}

#vepjlbijat .gt_footnote_marks {
  font-style: italic;
  font-weight: normal;
  font-size: 75%;
  vertical-align: 0.4em;
}

#vepjlbijat .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#vepjlbijat .gt_indent_1 {
  text-indent: 5px;
}

#vepjlbijat .gt_indent_2 {
  text-indent: 10px;
}

#vepjlbijat .gt_indent_3 {
  text-indent: 15px;
}

#vepjlbijat .gt_indent_4 {
  text-indent: 20px;
}

#vepjlbijat .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table">
  
  <thead class="gt_col_headings">
    <tr>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="time">time</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="Day 1">Day 1</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="Day 2">Day 2</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="time" class="gt_row gt_right"><div class='gt_from_md'><p>09:00-10:30</p>
</div></td>
<td headers="Day 1" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#overview-background-and-some-theory">Overview, Background and Some Theory</a></p>
</div></td>
<td headers="Day 2" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#text-correlations-and-regression-models">Text Correlations and Regression Models</a></p>
</div></td></tr>
    <tr><td headers="time" class="gt_row gt_right"><div class='gt_from_md'><p>11:00:12:30</p>
</div></td>
<td headers="Day 1" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#r-basics-repetition">R Basics Repetition</a></p>
</div></td>
<td headers="Day 2" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#supervised-classification-methods">Supervised Classification Methods</a></p>
</div></td></tr>
    <tr><td headers="time" class="gt_row gt_right"><div class='gt_from_md'><p>14:00-15:30</p>
</div></td>
<td headers="Day 1" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#obtaining-text-data">Obtaining Text Data</a></p>
</div></td>
<td headers="Day 2" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#unsupervised-classification-methods">Unsupervised Classification Methods</a></p>
</div></td></tr>
    <tr><td headers="time" class="gt_row gt_right"><div class='gt_from_md'><p>16:00-17:30</p>
</div></td>
<td headers="Day 1" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#dictionary-methods">Dictionary methods</a></p>
</div></td>
<td headers="Day 2" class="gt_row gt_left"><div class='gt_from_md'><p><a href="#word-embeddings-and-deep-learning">Word Embeddings and Deep Learning</a></p>
</div></td></tr>
  </tbody>
  
  
</table>
</div>

# Overview, Background and Some Theory

This session focuses on the general concepts in ACA, like
pre-processing, the documents-term-matrix, dimensionality reduction and
so on. It also provides a general overview on ACA-methods, how they are
implemented in software and what kinds of research questions and designs
are possible (or at least which have been asked before).

Additional Readings:

1.  Taking Stock of the Toolkit (Boumans and Trilling 2016)
2.  Text Analysis in R (Welbers, van Atteveldt, and Benoit 2017)
3.  Text as Data: The Promise and Pitfalls of Automatic Content Analysis
    Methods for Political Texts (Grimmer and Stewart 2013)
4.  Computer-Assisted Text Analysis for Comparative Politics (Lucas et
    al. 2015)

# R Basics Repetition

A brief run-through of some basic principles in `R`. I expect that you
have worked with `R` before and can already do some things. But even
after using R for a while, it doesn’t hurt to go over some fundamentals
and clear out common misunderstandings of the language. Covered
concepts:

- Installing packages, help files and other sources for help
- Writing functions
- Loops
- if statements
- Objects and classes in R
- R base vs Tidyverse
- Pipes in R
- ggplot2: core concepts and misunderstandings
- Important shortcuts in RStudio

Additional Readings:

1.  Advanced R (Wickham 2019a)
2.  ggplot2: Elegant Graphics for Data Analysis (Wickham 2019b)

# Obtaining Text Data

There are a myriad of ways to analyse text in `R`. If you ever want to
make use of them though you have to somehow get your own data into `R`.
This can be a bit boring and so this session might not be the most
impressive one. But by the end of it, you will be able to use your own
data in the coming sessions. And isn’t that exciting!

Key Points:

- Reading in common file formats (txt, PDF, docx and so on).
- Case 1: Use of newspaper data
- Case 2: Web-Scraping (a brief overview)
- Case 3: Twitter scraping (How to make an account, install rtweet)

Additional Readings:

- none; but think about what sources of text data you want to use and
  bring it along if possible.

# Dictionary Methods

Dictionary approaches belong to the oldest and simplest methods in ACA.
The key concept here is the dictionary, which is a list of words along
with a category, such as positive/negative sentiment, anger/joy,
geo-locations and so on. By checking if texts contain words from the
category, we can infer if each text belongs to the category defined in
the dictionary. In this session, we use a simple example and discuss the
pro and cons of dictionary methods.

Additional Readings:

- Text Mining with R chapter
  [2](https://www.tidytextmining.com/sentiment.html) (Silge and Robinson
  2020)

# Text Correlations and Regression Models

One of the fundamental ideas of ACA is that text is just another form of
data. Once we obtained the text and turned it into a
document-term-matrix, it is not fundamentally different from other forms
of statistical data any more. Therefore we can perform all sorts of
statistical analysis on it – like correlations and regressions. In this
session, we perform these techniques on example datasets to answer first
research questions.

Additional Readings:

- Text Mining with R chapter
  [4.1.4](https://www.tidytextmining.com/ngrams.html#visualizing-a-network-of-bigrams-with-ggraph)
  (Silge and Robinson 2020)
- Supervised Machine Learning for Text Analysis in R
  [6](https://smltar.com/mlregression.html) (Hvitfeldt and Silge 2021)

# Supervised Classification Methods

The idea behind supervised classification or supervised learning
approaches is that you train a model to emulate the behaviour of a human
coder. Specifically, a human classifies texts into categories, such as
positive/negative tone, spam/important emails and so on. By analysing
the statistical distribution of words in the two or more categories, a
model can predict the class of new unclassified material.

Additional Readings:

- Supervised Machine Learning for Text Analysis in R
  [7](https://smltar.com/mlclassification.html) (Hvitfeldt and Silge
  2021)

# Unsupervised Classification Methods

Unsupervised classification or unsupervised learning is a type of
machine learning where the computer is not given any labels or
categories to assign to data. Instead, the computer is tasked with
finding patterns and relationships in the data and then assigning
categories to the data based on those patterns. This is done through a
process called dimension reduction, which is similar to techniques like
Principal Component Analysis (PCA) or factor analysis. To use this
method, the researcher needs to define the number of categories they
want the computer to find and then interpret the results afterwards. One
of the most popular methods for unsupervised classification is Latent
Dirichlet Allocation (LDA) topic modeling. This method assigns a
probability to each word in a corpus to belong to a certain topic, and
then calculates the probability of each text in the corpus belonging to
a certain topic. In this way, the computer can find patterns and
relationships in the data and assign categories based on those patterns.

Additional Readings:

- Probabilistic topic models. (Blei 2012)
- Islamophobia and Media Portrayals of Muslim Women (Terman 2017)

# Word Embeddings and Deep Learning

This session introduces newer advances of text analysis that go beyond
traditional bag-of-words models. Word embeddings are a way to represent
words as vectors that capture their semantic meaning, and deep learning
models use neural networks to process and analyze text data. Students
will learn about popular word embedding algorithms like Word2Vec and
GloVe, as well as popular deep learning models for text analysis like
CNNs and RNNs. Through demonstrations, students will learn how to use
pre-trained word embeddings and implement simple deep learning models
for text classification. The session will also explore real-world
applications of these techniques in areas like sentiment analysis and
text classification.

Addional Readings:

- Supervised Machine Learning for Text Analysis in R
  [8-10](https://smltar.com/mlclassification.htmlhttps://smltar.com/dldnn.html)
  (Hvitfeldt and Silge 2021)

# References

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-bleiTopicModels2012" class="csl-entry">

Blei, David M. 2012. “Probabilistic Topic Models.” *Communications of
the ACM* 55 (4): 77–84. <https://doi.org/10.1145/2133806.2133826>.

</div>

<div id="ref-boumansTakingStockToolkit2016" class="csl-entry">

Boumans, Jelle W., and Damian Trilling. 2016. “Taking Stock of the
Toolkit: An Overview of Relevant Automated Content Analysis Approaches
and Techniques for Digital Journalism Scholars.” *Digital Journalism* 4
(1): 8–23. <https://doi.org/10.1080/21670811.2015.1096598>.

</div>

<div id="ref-grimmerTextDataPromise2013" class="csl-entry">

Grimmer, Justin, and Brandon M. Stewart. 2013. “Text as Data: The
Promise and Pitfalls of Automatic Content Analysis Methods for Political
Texts.” *Political Analysis* 21 (3): 267–97.
<https://doi.org/10.1093/pan/mps028>.

</div>

<div id="ref-SilgeMachineLearning2021" class="csl-entry">

Hvitfeldt, Emil, and Julia Silge. 2021. *Supervised Machine Learning for
Text Analysis in R*. <https://smltar.com/>.

</div>

<div id="ref-lucasComputerAssistedTextAnalysis2015" class="csl-entry">

Lucas, Christopher, Richard A. Nielsen, Margaret E. Roberts, Brandon M.
Stewart, Alex Storer, and Dustin Tingley. 2015. “Computer-Assisted Text
Analysis for Comparative Politics.” *Political Analysis* 23 (2): 254–77.
<https://doi.org/10.1093/pan/mpu019>.

</div>

<div id="ref-SilgeTextMining2020" class="csl-entry">

Silge, Julia, and David Robinson. 2020. *Text Mining with R*.
<https://www.tidytextmining.com/>.

</div>

<div id="ref-termanIslamophobia2017" class="csl-entry">

Terman, Rochelle. 2017. “Islamophobia and Media Portrayals of Muslim
Women: A Computational Text Analysis of US News Coverage.”
*International Studies Quarterly* 61 (3): 489–502.
<https://doi.org/10.1093/isq/sqx051>.

</div>

<div id="ref-welbersTextAnalysis2017" class="csl-entry">

Welbers, Kasper, Wouter van Atteveldt, and Kenneth Benoit. 2017. “Text
Analysis in R.” *Communication Methods and Measures* 11 (4): 245–65.
<https://doi.org/10.1080/19312458.2017.1387238>.

</div>

<div id="ref-wickhamgadvancedr2019" class="csl-entry">

Wickham, Hadley. 2019a. *Advanced r*. <http://adv-r.had.co.nz/>.

</div>

<div id="ref-wickhamggplot22019" class="csl-entry">

———. 2019b. *Ggplot2: Elegant Graphics for Data Analysis*.
<https://ggplot2-book.org/>.

</div>

</div>
