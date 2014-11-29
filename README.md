# Drupal JMeter Tricks #

**Author: [Erik Webb](http://www.erikwebb.net/)**

## Requirements ##

- JMeter 2.12+ [[Download](https://jmeter.apache.org/download_jmeter.cgi)]
    - *Ensure the `jmeter` script is in your PATH and executable*
- JMeter Plugins [[Download](http://jmeter-plugins.org/)]
- A Drupal 7 site

### Test Site Setup ###

To setup a simple site for testing these JMeter scripts, use the following Drush commands -

    drush site-install --account-name="admin" --account-pass="admin" \
        --site-name="Drupal JMeter Test" standard
    drush user-create user --password="user"

## Running ##

A simple `Rakefile` is included to simplify a few commands -

- **rake edit**: Open the JMX file in JMeter.
- **rake run**: (Default) Run the JMX file and output results to `results.jtl`.
- **rake analayze**: (Currently unsupported) Analyze the results stored in `results.jtl`.

## Contents ##

- **drupal-jmeter-tricks.jmx**: Sample JMeter test script with multiple thread groups to illustrate different techniques. The following scenarios are used as examples -
    1. **Drupal Login**: Login as a Drupal user, driven by a CSV file.
    1. **Select From A List**: View a content listing and select a single item at random to view.
    1. **Traverse Menu Tree**: Visit every page located in the main menu.
    1. **Create a Node**: Save a new piece of content using hard-coded values.
    1. **Visit List of URLs**: Visit every URL listed in a CSV file.
- **jmeter.properties**: Properties needed for a usable results file.
- **Rakefile**: Rake file to shortcut common tasks.
- **users.csv**: Sample user dictionary file
- **urls.csv**: Sample list of URLs to test against

## Explanations ##

There are a few configuration settings that require specific note here -

1. XPath query used to detect a Drupal error message -

        //div[contains(concat(' ',normalize-space(@class),' '),' messages ') and contains(concat(' ',normalize-space(@class),' '),' error ')]

1. Choosing a random item from a JMeter list returned by the XPath Post Processor -

        ${__V(node_links_${__Random(1,${node_links_matchNr})})}

1. Check if a variable was successfully set -

        "${node_links}".length > 0
