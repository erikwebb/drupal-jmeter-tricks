# Drupal JMeter Tricks #

**Author: [Erik Webb](http://erikwebb.net/)**

## Requirements ##

- JMeter 2.7+ [[Download](https://jmeter.apache.org/download_jmeter.cgi)]
- JMeter Plugins [[Download](https://code.google.com/p/jmeter-plugins/)]
- A Drupal 7 site

## Contents ##

- *drupal-jmeter-tricks.jmx*: Sample JMeter test script with multiple thread groups to illustrate different techniques.

  - *Drupal Login*: Login as a Drupal user, driven by a CSV file.
  - *Select From A List*: View a content listing and select a single item at random to view.
  - *Traverse Menu Tree*: Visit every page located in the main menu.
  - *Create a Node*: Save a new piece of content using hard-coded values.
  - *Visit List of URLs*: Visit every URL listed in a CSV file.

- *users.csv*: Sample user dictionary file
- *urls.csv*: Sample list of URLs to test against

## Explanations ##

There are a few configuration settings that require specific note here -

1. XPath query used to detect a Drupal error message -

        //div[contains(concat(' ',normalize-space(@class),' '),' messages ') and contains(concat(' ',normalize-space(@class),' '),' error ')]

1. Choosing a random item from a JMeter list returned by the XPath Post Processor -

        `${__V(node_links_${__Random(1,${node_links_matchNr})})}`

