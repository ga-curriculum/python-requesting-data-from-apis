<h1>
  <span class="headline">Exploring APIs with Python</span>
  <span class="subhead">Making an HTTP Request</span>
</h1>

**Learning objective:** By the end of this lesson, learners will be able to **utilize** the Python `requests` library to send HTTP requests and **extract** relevant data from the response.

| Lesson                    | Duration |
| ------------------------- | -------- |
| Requesting Data From APIs | 15 min   |

<br>

<div class="activity guided-walkthrough">
  <h2 class="title">Requesting Data From APIs</h2>
  <span class="minutes">15 min</span>
</div>

<br>

Let's practice making an API call in Python. We'll start by using a fun and free API (no key required) called [The Cat Fact API](https://catfact.ninja/).

First we'll import Python's `requests` library, and define our API url endpoint. Next, we'll make a simple `GET` request to see all breeds available in their database.

```py
import requests

# Define the API endpoint
url = 'https://catfact.ninja/breeds'

# Send the GET request
response = requests.get(url, timeout=10)

# Check the response status
print(response.status_code)  # Should return 200 for a successful request
```

## Handling the Response

Once the request is successful, the data returned in JSON format. The `requests` library can automatically convert this to a Python dictionary using the `.json()` method.

```py
# Parse the response data as JSON
data = response.json()

# Print the entire response
print(data)
```

> 💡 The `.json()` method simplifies working with API data by converting it to Python's dictionary structure.

### Sample data response

```json
{
  "data": [
    {
      "breed": "Abyssinian",
      "country": "Ethiopia",
      "origin": "Natural/Standard",
      "coat": "Short",
      "pattern": "Ticked"
    },
    {
      "breed": "Aegean",
      "country": "Greece",
      "origin": "Natural/Standard",
      "coat": "Semi-long",
      "pattern": "Bi- or tri-colored"
    },
    {
      "breed": "American Curl",
      "country": "United States",
      "origin": "Mutation",
      "coat": "Short/Long",
      "pattern": "All"
    }
  ]
}
```

## Navigating Complex Data

The API response might contain nested structures like lists and dictionaries. Let's see how to access specific data.

```py
# Accessing a specific item from the data
print(data['data'][0]['breed'])  # Outputs the breed of the first cat
```

> 💡 Try accessing other properties like the country or coat for the second cat in the list.

## Verifying the Structure

It's important to verify the structure of the response when working with unfamiliar APIs. Use `type()` to ensure you're working with the expected data types.

```py
# Verify the structure of the response
print(type(data['data']))  # Should return <class 'list'>
```

## Example Error Handling

Sometimes, you may accidentally try to access data that doesn't exist. This can lead to an error.

```py
# Example: Accessing an index that is out of range
try:
    print(data['data'][3]['breed'])
except IndexError:
    print("The index is out of range.")
```

> 💡 Add a `try-except` block to handle potential errors when navigating data.
