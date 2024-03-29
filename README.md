# Seqwa Search API Implementation

## About Seqwa

Seqwa is a low-cost, easy-to-use, hosted search platform for solving your critical search requirements. It supports three uniquely beneficial functions: Autocomplete (query suggestions and top Full-text Search results), Search (Full-text Search with Semantic Ranking for intent), and Recommend (Intent-driven Semantic Search). Work with one or all the functions based on your needs. Set up a functional search utility in minutes: upload your data, generate API keys, publish a demo user interface, and search. Enjoy a seamless search experience supported by a highly available and scalable cloud infrastructure.

To learn more, please visit: https://www.seqwa.com/

## Tech Stack

- [ReactJS](https://reactjs.org/)
- [Java](https://www.java.com/)
- [SpringBoot](https://spring.io/projects/spring-boot)
- [TailwindCSS](https://tailwindcss.com/)
- [HeadlessUI](https://headlessui.dev/)
- [Seqwa](https://www.seqwa.com/)

## Search

Search function integrates full-text search with semantic ranking to provide better search results based on context or user preferences. Semantic ranking personalizes full-text search results for products based on user browsing or purchase history. It includes support for double-quoted phrases for specificity and AND/OR/NOT operators for filtering.

### Request URL

https://www.seqwa.com/api/v1/search

### Method

GET

### Headers

| Header        | Description                            |
| ------------- | -------------------------------------- |
| Content-Type  | application/json                       |
| seqwa-api-key | API KEY generated for the Search       |

### Function

#### Params

| Param          | Description                                                                                                                                                                                                         | Required |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| index          | Index Id                                                                                                                                                                                                            | required |
| query          | Query text entered by the user. Supports Lucene query parser syntax which includes AND, OR, and NOT operands, term query like fieldName:fieldValue, and range query like fieldName:[minFieldValue TO maxFieldValue] | required |
| highlightField | Field for highlighting the query text                                                                                                                                                                               | optional |
| fields         | Array of fields                                                                                                                                                                                                     | optional |
| type           | Takes the options: ranked and unranked. (Default: unranked)                                                                                                                                                                                                | optional |
| context        | Contextual text for personalization with semantic ranking. The type MUST be set as ranked to apply the context.                                                                                                                                                                                                 | optional |
| maxResults     | Maximum results to be returned. (Default: 100, Limit: 200)                                                                                                                                                          | optional |

#### Request URL Structure

```
https://www.seqwa.com/api/v1/search
?index=INDEX_ID&query=QUERY_TEXT
&highlightField=SEARCH_FIELD&fields=FIELDS&type=RANKING_TYPE
&context=CONTEXT&maxResults=MAX_RESULTS
```

#### Response

| Object       | Description                                                                                                                                                                                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| searchResults  | Contains an array of search results for queries based on the query text. Each element of the array is an object with recordId, summary, displaySummary, and requested fields as parameters. The summary param is plain text and displaySummary has highlighted words with the html `<b>` element. |
| topTags  | Contains an array of top tags from the search results.     
| error        | Returns an error message if any error occurs on the server.                                                                                                                                                                                                  |

#### Response JSON Structure

```
{
  "searchResults": [
    {
      "recordId": "##",
      "summary": "...",
      "displaySummary": "<b>....</b> ...",
      "field1": ".....",
      "field2": ".....",
      "field3": "....."
    },
    {
      "recordId": "##",
      "summary": "...",
      "displaySummary": "<b>....</b> ...",
      "field1": ".....",
      "field2": ".....",
      "field3": "....."
    }
  ],
  "topTags": [
    "...",
    "..."
  ],
  "error": "....."
}
```
