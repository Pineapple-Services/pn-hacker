# 🎚 pn-hud Documentation
This guide provides instructions on how to customize **pn-hacker**.

---

## Table of Contents
1. [Dependencies](#dependencies)
2. [Commands](#commands)
3. [Modules](#modules)

---

## Dependencies
- [ox_lib](https://github.com/overextended/ox_lib)
- [ox_inventory](https://github.com/overextended/ox_inventory)
- [pma-voice](https://github.com/AvarianKnight/pma-voice) or [saltychat](https://github.com/v10networkscom/saltychat-fivem/)
- [lb-phone](https://lbscripts.com/) or [qb-phone](https://github.com/qbcore-framework/qb-phone) _(to check if your phone could be integrated open a ticket on our discord)_

---

## Commands
### ❓ How to create commands?
1. Go to `pn-hacker/client/commands`
2. Create a lua file `{command name}.lua`
3. Now, you can follow the base given on `example.lua` *for custom commands / modules open a ticket on our discord*
4. Develop your custom command!

**Example Command:**
```lua
Commands["example"] = { -- command name (it will execute using this name)
    description = "Delete 'client/commands/example.lua' to remove me :O", -- command description
    usage = "example <echo|getinput|hasitem>", -- command usage
    canUse = function()
        return true -- check if player can use command (do ur own checks)
    end,
    onUse = function(args, handle) -- what will happen when the player executes the command?
        if #args <= 0 then
            API.UI.SendMessage(("Usage: %s"):format(Commands["example"].usage))
            return
        end

        local action = args[1]

        if action == "echo" then
            local messageToEcho = args[2] or "No message provided."
            API.UI.SendMessage(("Echoed message: %s"):format(messageToEcho))
        elseif action == "getinput" then
            local input = API.UI.GetInputFromConsole()
            API.UI.SendMessage(("Player said %s\nOhh.. forgot to tell you..\n\nI'll clear the console in 2.7 seconds!"):format(input))
            Wait(2700)
            API.UI.ClearConsole()
        elseif action == "hasitem" then
            local hasBread = API.Utils.HasItem("bread")
            local message = hasBread and "Why the fuck do you have a bread in your computer storage?" or "Oh thank god, you're normal!"
            API.UI.SendMessage(message)
        else
            API.UI.SendMessage("Invalid action. Use 'echo', 'getinput' or 'hasitem.")
        end
    end
}
```
---

## Modules  
### Available Modules  
- pn-receiver *(included in the package)*

❓ Are you a **developer** and you want to put your script here? Just join our Discord server and notice us.


### How to create a module?
1. You can follow our base by clicking right here

---

## API
You can use this **API** to develop [Commands](#commands) and [Modules](#modules), but also for a general knowledge to edit the script in case you bought open source.

### Get API Object
```lua
local API = exports["pn-hacker"]:API()
```

### Utils
```lua
local input = "hello world" -- example input string
local args = API.Utils.ParseArgs(input) -- divides input in args (example in pn-module-example)
print(args[1]) -- Output: "hello"
print(args[2]) -- Output: "world"

local gotItem = API.Utils.HasItem("bread") -- checks if it got "bread" in tablet's storage.
```

### UI
```lua
API.UI.ClearConsole() -- clears the entire console
API.UI.SendMessage("Hello World!") -- sends "Hello World!" to the player's console.

local input = API.UI.GetInputFromConsole() -- gets input from console
print(input) -- prints what u texted in the console input, does not count commands obviously.
```

### Modules
```lua
local isInModule = false

API.Modules.create({
    name = "example_module_name",
    action = function()
        isInModule = true
        while isInModule do
            local input = API.UI.GetInputFromConsole()
            local args = API.Utils.ParseArgs(input)

            if args[1] == "exit" then
                isInModule = false
            else
                API.UI.SendMessage("Invalid module command.")
            end
        end
    end,
    canUse = function()
        return API.Utils.HasItem("example_module_item") -- in this case im checking if it got an item in the storage, but you can check whatever u want
    end,
})
```
