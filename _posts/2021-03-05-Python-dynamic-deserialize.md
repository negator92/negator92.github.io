---
layout: post
title: Python dynamic deserialize
---

First of all, I must warn you: the explicit is better than the implicit.

Since I needed to deserialize a certain amount of data from a json file, I ran into the problem that today I have 3 key-value pairs, tomorrow there are 5, and by the end of the month there may be 11 of them.
I didn't want to describe so many fields in the class constructor, and since my json file contains only settings, usernames, passwords, and tokens (I will definitely hash them instead of storing them in an open strings), I know what to expect to get from the file.

I used the following construction for such a codehack to get the desired result:

---
~~~import json

class ClassName(object):
    def __init__(self, j):
        self.__dict__ = json.loads(j)

with open('Configuration.json', 'r', encoding='utf-8') as configFile:
    jsonStr = configFile.read()

config = Configuration(jsonStr)

print(config.username)
print(config.password)
print(config.token)
~~~
---

This allowed me to avoid writing scary references to the dictionary element.
Nevertheless, I must repeat that the explicit is better than the implicit. The fact that I have to write in a dynamic language relaxes me too much and makes me lazy, although I understand that in C# I would describe every field, perhaps I would also use attributes (but this is not accurate, lol).