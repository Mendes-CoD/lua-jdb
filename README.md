# Lua Json DataBase

JDB is a is a simple library to work with json database

## Requires
| Lib | GitHub |
| ------ | ------ |
| Underscore | https://github.com/mirven/underscore.lua |
| Json | https://github.com/rxi/json.lua |

## Usage

```lua
    local db = require('jdb').init(path/to/file) -- Retrun all function
```

##### Inserting json string to file (database)

```lua
    db.insert(table) -- Retrun true if the operation was successful or nil
```

##### Remove json string

```lua
    db.remove(table) -- Retrun true if the operation was successful or nil
```

##### Finding all json string

```lua
    db.find(table) --  Retruns a table of elements if the operation was       successful or nil
```

##### Get all file (database)

```lua
    db.getAll() --  Retrun all file (database)
```

## Example

##### test.json

```json
{"name": "BBooGG", "age": 25}
{"name": "molimawka", "age": 25}
{"name": "crashmax", "age": 35, "color":{"r": 0, "g": 165, "b": 255}}
```

##### example.lua

```lua
    local db = require('jdb').init('test.json')
    
    local gAll = db.getAll()
    print(gAll) --[[
    {
        {
            name = "BBooGG",
            age = 25
        },
        {
            name = "molimawka",
            age = 25
        },
        {
            name = "crashmax",
            age = 35,
            color = {
                r = 0,
                g = 165,
                b = 255
            }
        }
    }
    ]]
    
    local ins = db.insert({name = "Lesha"})
    print(ins) -- true
    
    local insError = db.insert('string')
    print(insError) -- nil
    
    local rem = db.remove({name = "Lesha"})
    print(rem) -- true
    
    local remError = db.insert({name = "Jon"})
    print(remError) -- nil
    
    local remError2 = db.insert('string')
    print(remError2) -- nil
    
    local f1 = db.find({name = "molimawka"}) 
    print(fi) --[[
    {
        {
            name = "molimawka",
            age = 25
        }
    }
    ]]
    
    local f2 = db.find({age = 25}) 
    print(f2) --[[
    {
        {
            name = "BBooGG",
            age = 25
        },
        {
            name = "molimawka",
            age = 25
        }
    }
    ]]
    
    local f3 = db.find({color = {
            b = 255
        }
    }) 
    print(f3) --[[
    {
        {
            name = "crashmax",
            age = 35,
            color = {
                r = 0,
                g = 165,
                b = 255
            }
        }
    }
    ]]
```