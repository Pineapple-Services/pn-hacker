# 🎚 pn-hud Documentation
This guide provides instructions on how to customize **pn-hacker**.
---
## Table of Contents
1. [Dependencies](#dependencies)
2. [Commands](#commands)
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
Commands["example"] = {
    description = "Delete 'client/commands/example.lua' to remove me :O",
    usage = "example <echo|getinput|hasitem>",
    onUse = function(args, handle)
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
