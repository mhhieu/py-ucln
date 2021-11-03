# Important Stuff, trust!!! :

## Balance between readability, scalability[1] and optimizations
- This section doesn't undervalue the practicality of making your game performant, but overestimating the impact of some optimizations and implementing them can waste time and harm readability alongside overall ability of your code. A micro optimization is an optimization that doesn't **add up**, below is an example of micro optimized code vs regular code.

```lua
local InputService = game:GetService("UserInputService")
local Remotes = game.ReplicatedStorage.Remotes -- not using :GetService() because they're afraid of a function call

if 2 < Variable then -- uses "<" because ">" translates to "<", a very micro optimization

end

-- vs

local InputService = game:GetService("UserInputService")
local Remotes = game:GetService("ReplicatedStorage").Remotes -- staying consistent with the usage of :GetService() above

if Variable > 2 then -- placing the longer expression on the left can improve readability but you lose 1 nanosecond though :CCCCCC

end
```

- Readable code is crucial especially when you want to present it to other people(or if you're working in a team) or when you go back to tweak it after a while so its semantics[2] can be analyzed quickly.

```lua
local PascalCase = true
local inconsistent_Casing = true
local function veryUselessFunction()
    local CLD = "short for cooldown"
    if CLD=="1" then
        local pos = Vector3.new(1,1,1)
    end
    return "idk man"
end

-- vs

local PascalCase = true
local InconsistentCasing = false

local function UselessFunction()
    local Cooldown = "Cooldown"

    if Cooldown == "1" then
        local Position = Vector3.new(1, 1, 1)
    end

    return "ik man"
end
```

- Use conventional and idiomatic methods to avoid confusion, also because they're likely to get optimized[3].

Here's a few examples of non-idiomatic vs code idiomatic

```lua
Table[#Table + 1] = "hi" -- bad

table.insert(Table, "hi") -- good
```

```lua
-- bad

local function Iterate(Array, Index)
    Index = (Index and Index + 1) or 1

    return Table[Index], Index
end

for i, v in Iterate, Table do

end

-- good

for i, v in ipairs(Table) do

end
```

Here's an example of unconventional and conventional code

```lua
for i = 1, #Array do -- bad
    local v = Array[i]
end

for i, v in ipairs(Array) do -- good
    
end
```


## Comments
- Using comments can help make your code more readable, or the opposite. Comments should be used to guide the reader like avoiding semantical confusion instead of telling what part of the code does what. In the following example(for some reason the person decided to overcomplicate the if statement), it shows what should be avoided and what could be done instead.

*Bad use of comments :*

```lua
-- Variables

local Humanoid = Humanoid -- this is where the humanoid is declared

-- Events

Humanoid.Running:Connect(function(Speed) -- fires when the humanoid runs
    if not (Speed <= 0) then -- Checks if the player is still moving because the event fires when the player stops walking
        -- do something
    end
end)
```

*Okay use of comments :*

```lua
local Humanoid = Humanoid

Humanoid.Running:Connect(function(Speed)
    if not (Speed <= 0) then -- not has a higher operator priority(like PEDMAS) so removing the parentheses would cause the script error
        
    end
end)
```

## DRY(Don't Repeat Yourself)
- Declare a variable for something that you're using multiple times, use loops and functions for repeated tasks, don't insert scripts in every door and make a door handling module instead, etc.

 * If you had to handle a group of NPCs, then you should be looping through each npc and handle them accordingly like this :

```lua
local function Attack(Attacker, Target)
    -- do stuff
end

while true do
    for _, Mob in ipairs(List) do
        if WithinRange then
            Attack(Mob, Target)
        end
    end

    wait(1)
end
```

 * Instead of using individual scripts for every NPC like this :

```lua
while true do
    if WithinRange then
        -- do stuff
    end

    wait(1)
end
```

## OOP
- OOP is a programming paradigm, this part assumes you already know what it is so skip it if you don't know what OOP is.

- I see people overuse OOP all the time in the case of Roblox scripting. It should be used when OOP has more benefits then its alternative like when the use of methods is crucial. It could also be used when you're working with other scripters to facilitate usage of your co-workers' code. It's useful when making open sourced code as well.

## Being stuck
- It's easy to dig yourself in a bottomless pit by taking bad approaches then slapping bandaids constantly, to avoid getting stuck it's important to write code concisely like not rushing.

- If you're stuck, get some help.

- Touch some grass will ya?

## Improvement
- If you've written some code, it's a good idea to receive feedback from an outer perspective to further improve it while also learning something new.

## Annex
* [1] The ability of a computing process to be used or produced in a range of capabilities
* [2] The meaning of a word, phrase, sentence, or text
* [[3]](https://luau-lang.org/performance)
