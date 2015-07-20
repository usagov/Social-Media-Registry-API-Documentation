# Social Media Registry API Documentation

## On This Page
*   [About the API](#about-the-api)
*   [Accessing the API](#accessing-the-api)
*   [API Methods](#api-methods)
*   [Source Code](#source-code)
*   [Example Applications](#example-applications)
*   [Terms of Service](#terms-of-service)

## About the API
This documentation describes methods to use the Social Media Registry API to access the contents of the [Social Media Registry](https://www.usa.gov/verify-social-media).

The [Social Media Registry](https://www.usa.gov/verify-social-media) is an official source of information about social media accounts that represent official U.S. federal government agencies, elected officials, or members of the President’s Cabinet.

If you work for the federal government and have a .gov or .mil e-mail address, you can register official U.S. federal accounts at [DigitalGov.gov](http://www.digitalgov.gov/services/social-media-registry/).

If you have feedback, questions, or want to tell us about the product you built with the Social Media Registry API, please [e-mail us](mailto:socialmediaregistry@gsa.gov).

## Accessing the API

The interface described here uses the same method URLs and parameters for all response formats, including HTML5, JSON, and XML. If no response format is specified at request time, the results are returned as HTML5 (with the assumption that a user is accessing the API via a web browser). To specify alternate formats, append the result format to the method call:

* [http://registry.usa.gov/accounts?agency_id=usda](http://registry.usa.gov/accounts?agency_id=usda)  
* [http://registry.usa.gov/accounts.json?agency_id=usda](http://registry.usa.gov/accounts.json?agency_id=usda)  
* [http://registry.usa.gov/accounts.xml?agency_id=usda](http://registry.usa.gov/accounts.xml?agency_id=usda)  

API requests can be called from remote sites via Javascript using the [Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) mechanism (CORS) supported in most browsers. All published API methods may be called from any domain.

If support for older browsers is required, JSON requests can be made with a callback parameter in order to return JSONP responses:

[http://registry.usa.gov/accounts.json?agency_id=usda&callback=listaccounts](http://registry.usa.gov/accounts.json?agency_id=usda&callback=listaccounts)

### API Updates Using Feeds

Some API methods are also available as feeds in the ATOM format. These feeds can be added to any news feed reader to list recent changes.

The ATOM format is an XML feed standard; each entry contains a summary of the Registry change and a link to the Registry API to view more information.

**Feed Examples**

List the most recently updated official Twitter accounts: [http://registry.usa.gov/accounts.atom?service_id=twitter](http://registry.usa.gov/accounts.atom?service_id=twitter)

List the most recently updated official accounts from the U.S. Department of Agriculture: [http://registry.usa.gov/accounts.atom?agency_id=usda](http://registry.usa.gov/accounts.atom?agency_id=usda)

## API Methods

### /accounts (GET)

List official U.S. government social media accounts entries in the registry. This method is also available as an ATOM feed.

**Parameters**

*   agency_id: ID (from /agencies)
*   service_id: ID (from /services)
*   tag: text
*   page_size: integer
*   page_number: integer

**Output**

*   page_count: integer
*   page_number: integer
*   total_items: integer

**Accounts**

*   service_url: text
*   verified : boolean
*   service_id: ID
*   account: text
*   details_url: text
*   organization: text
*   agencies
    *   agency_id: text
    *   agency_name: text
    *   agency_url: text

**Example Calls**

List all official accounts from the U.S. Department of Agriculture: [http://registry.usa.gov/accounts?agency_id=usda](http://registry.usa.gov/accounts?agency_id=usda)

List all official Twitter accounts from the U.S. Department of Health and Human Services:
[http://registry.usa.gov/accounts?service=twitter&agency_id=hhs](http://registry.usa.gov/accounts?service=twitter&agency_id=hhs)

### /accounts/{service ID} (GET)

A synonym for /accounts?service_id={service}, provided for REST-style browsing.

### /accounts/{service ID}/{account} (GET)

A synonym for the /accounts/verify method, using a canonical service and account ID provided by that method. For example, the service and account ID for http://twitter.com/JPL_Bear might be twitter/JPL_Bear, making the canonical URL take the form [http://registry.usa.gov/accounts/twitter/JPL_Bear](http://registry.usa.gov/accounts/twitter/JPL_Bear)

This is provided primarily for REST-style browsing.

### /accounts/verify (GET)

Check whether the provided URL is registered as an official government social media account.

Example: /accounts/verify?service_url=https%3A%2F%2Ftwitter.com%2F%23%21%2FJPL_Bear

**Parameters**

*   service_url: URL (required)

**Output**

*   verified: boolean
*   service_url: URL
*   service_id: ID (from /services list)
*   account: text

(if verified is true:)

*   details_url: URL
*   organization: text
*   info_url: text
*   agencies
    *   agency_id: text
    *   agency_name: text
    *   agency_url: text
*   tags: list
*   language: text
*   display_name: text
*   updated_by: text
*   updated_at: ISO 8601 date

### /agencies (GET)<a id="agenciesapi" name="agenciesapi"> </a>

List the sponsoring agencies that may be specified in the /accounts/add method.

**Parameters**

*   none

**Output**

*   page_count: integer
*   total_items: integer
*   page_number: integer
*   agencies: list
    *   agency_id: text
    *   agency_name: text
    *   agency_url: text

### /services (GET)

List the social media services that are currently supported in the /accounts/add method.

**Parameters**

*   none

**Output**

*   page_count: integer
*   total_items: integer
*   page_number: integer
*   services: list
    *   service_id: text
    *   service_name: text

### /tags (GET)<a id="tags" name="tags"> </a>

List tags that are suggested for describing an account.

**Parameters**

*   keywords: text

**Output**

*   tags: list
*   tag_id: text
*   tag_text: text

## Source Code

The code for the Social Media Registry is open source and available on [GitHub](https://github.com/usagov/ringsail). It is written in Ruby.

## Example Applications

*   [Embeddable Twitter Widgets](http://www.digitalgov.gov/services/social-media-registry/#Twitter-List-Widget) – A suite of dynamic widgets that aggregate tweets from cabinet departments and by topic.
*   [Federal Government YouTube Videos](http://search.usa.gov/search/news?query=+&channel=867&affiliate=youtube) – A chronological listing of federal government videos on YouTube. Search is available.
*   [Federal Open Source Projects on GitHub](http://gsa.github.com/federal-open-source-repos/) – A dynamic list of the public repositories from federal government GitHub accounts.
*   [Great Gov Tweets](http://shiningsea.measuredvoice.com) - A daily list of the top 50 tweets published by federal Twitter accounts.

## Terms of Service

By using this data, you agree to the [Terms of Service](https://www.usa.gov/developer-terms-of-service).
