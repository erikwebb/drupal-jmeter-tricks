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

    > rake -T
    rake analyze  # Perform log analysis on JMeter results
    rake clean    # Remove current log and results files
    rake edit     # Open JMeter script for editing
    rake json     # Save the results.jtl file as JSON
    rake run      # Run JMeter script and save results

## Contents ##

- **test.jmx**: Sample JMeter test script with multiple thread groups to illustrate different techniques. The following scenarios are used as examples -
    1. **Drupal Login**: Login as a Drupal user, driven by a CSV file.
    1. **Select From A List**: View a content listing and select a single item at random to view.
    1. **Traverse Menu Tree**: Visit every page located in the main menu.
    1. **Create a Node**: Save a new piece of content using hard-coded values.
    1. **Visit List of URLs**: Visit every URL listed in a CSV file.
    1. **Visit List of 404 URLs**: Visit every 404 URL listed in a CSV file.
    1. **Clear Cache**: Login as an admin and clear the Drupal caches.
- **jmeter.properties**: Properties needed for a usable results file.
- **Rakefile**: Rake file to shortcut common tasks.
- **users.csv**: Sample user dictionary file
- **urls.csv**: Sample list of URLs to test against

> NOTE: In order to [optimize resource utilization](http://jmeter.apache.org/usermanual/listeners.html#resources), only a [Simple Data Writer](http://jmeter.apache.org/usermanual/component_reference.html#Simple_Data_Writer) listener is used. The fields stored in `results.jtl` file are configured using `jmeter.properties`.

### Explanations ###

There are a few configuration settings that require specific note here -

1. XPath query used to detect a Drupal error message -

        //div[contains(concat(' ',normalize-space(@class),' '),' messages ') and contains(concat(' ',normalize-space(@class),' '),' error ')]

1. Choosing a random item from a JMeter list returned by the XPath Post Processor -

        ${__V(node_links_${__Random(1,${node_links_matchNr})})}

1. Check if a variable was successfully set -

        "${node_links}".length > 0

## Issues ##

If you have run into issues, please [post an issue on Github](https://github.com/erikwebb/drupal-jmeter-tricks/issues/new) and attach your `jmeter.log` file.
