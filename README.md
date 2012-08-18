# Drupal JMeter Tricks #

## Requirements ##

- JMeter 2.7+ [[Download](https://jmeter.apache.org/download_jmeter.cgi)]
- JMeter Plugins [[Download](https://code.google.com/p/jmeter-plugins/)]
- A Drupal 7 site

## Contents ##

- *tests.jmx* => Sample JMeter test script with multiple thread groups to illustrate different techniques
- *users.csv* => Sample user dictionary file
- *urls.csv* => Sample list of URLs to test against

## Explanations ##

There are a few configuration settings that require specific note here -

1. XPath query used to detect a Drupal error message -

`//div[contains(concat(' ',normalize-space(@class),' '),' messages ') and contains(concat(' ',normalize-space(@class),' '),' error ')]`

1. Choosing a random item from a JMeter list returned by the XPath Post Processor -

`${__V(node_links_${__Random(1,${node_links_matchNr})})}`

