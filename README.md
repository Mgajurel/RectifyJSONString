# RectifyJSONString

This is an approach to handle json string before you feed it to json.loads()

It is seen that json implementation for python2 can simply only escape special characters and single quotes based on the type of the encoding that you use. But there is no any deliberate solution to escape double quotes when they are present within the value of a json string.
#ILLUSTRATION:

Consider a json string in unicode and if you try to load it using json module as:

```python
import json

json_string = u'''
{
"name" : "James",
"description" : "I am a \"Boy\""
}
'''
# json loads only takes a string, bytes or byte stream
json_string = json_string.decode('utf-8')

# We try loading the string
json.loads(json_string)
```

You get an error as:

```python
ValueError: Expecting ',' delimiter: line 4 column 26 (char 46)
```

Which is simply because your string is unicode and decode (in json) doesn't escape double quotes.

The approach followed here is an iterative one, It tries to fix the json by iteratively finding the unescaped double quotes and escaping it for you so that you do not get any error as mentioned above.

#NOTE:

### It is just a desperate solution to a problem, communities' support is highly appreciated
