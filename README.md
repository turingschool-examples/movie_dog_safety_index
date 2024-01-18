# Movie Dog Safety Index

We've all been there. Watching the newest, latest movie with a cute dog in it, and all of a sudden, some villain hurts the dog. WHO would want to watch this?! Not me. 

The purpose of this API is to provide a way to check whether or not the dog survives the movie (if present). 

This API will consume [Does the Dog Die API](https://www.doesthedogdie.com/dddsearch), which is a crowdsourced database of movies with user comments and votes on the movie's canine cast welfare. 

## Setup
1. Fork and clone this repo. 
2. Setup: `bundle install && rails db:{create}`
3. You will need to sign up for an API Key and add it to this application. We recommend using `Rails application credentials` to store your API key. 

## Requirements
* Use Webmock and/or VCR to stub your request tests. 
* No data should be stored locally in this database. Always utilize the API data. 
* Returned data should be serialized to JSONAPI specifications. 
* Error handling should be utilized to create sad paths for each endpoint. 

# Assignment

Build an endpoint that will retrieve the users' votes for a specific movie by its title. 

Your endpoint shoudl follow this format: 

`GET /api/v1/movie?title=Old+Yeller`

Your API will return: 
* Movie information, including
  * Name
  * Genre
  * Release Year
  * Overview
* A key-value pair named `does_the_dog_die`.
  * Based on the user-provided "stats", you will need to find a way to programmatically comb through the returned stats and tally up all the votes between `definitely_yes` and `definitely_no`. 
  * Your API should return either `yes` or `no`, based on the highest number of votes.  
  * If the vote is tied or equal to 0, return `unknown`. 

Sample response: 


```json
{ 
   "data": {
      "id": "null",
      "type": "movie",
      "attributes": {
         "name": "Old Yeller",
         "genre": "adventure",
         "release_year": 1957,
         "overview": "Young Travis Coates is left to take care of the family ranch with his mother and younger brother while his father goes off on a cattle drive in the 1860s. When a yellow mongrel comes for an uninvited stay with the family, Travis reluctantly adopts the dog.",
         "does_the_dog_die": "yes"
      }
   }
}

```

### Sad Path - Movie with no dog or tied vote

`GET /api/v1/movie?title=Homeward+Bound`

Sample response: 

```json
{ 
   "data": {
      "id": "null",
      "type": "movie",
      "attributes": {
         "name": "Homeward Bound: the Incredible Journey",
         "genre": "adventure",
         "release_year": 1993,
         "overview": "Remake of the popular Disney classic, this time featuring some well known voices as two dogs and a cat trek across America encountering all sorts of adventures in the quest to be reunited with their owners.",
         "does_the_dog_die": "no"
      }
   }
}

```


