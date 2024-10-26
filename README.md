```lua
-- list to hold scripts and their delays
local scripts = {}

-- function to add a script with optional delay
local function addScript(scriptFunc, delay)
table.insert(scripts, {func = coroutine.create(scriptFunc), delay = delay or 0, startTime = os.clock()})
end

-- function to run all scripts
local function runAllScripts()
local function execute()
local active = false
local currentTime = os.clock()

for _, script in ipairs(scripts) do
if coroutine.status(script.func) ~= "dead" then
if currentTime - script.startTime >= script.delay then
active = true
local success, message = coroutine.resume(script.func)
if not success then print("Error: " .. message) end
end
end
end

if active then
game:GetService("RunService").Heartbeat:Wait()
execute()
else
print("All scripts executed.")
end
end
execute()
end

-- ADD YOUR SCRIPTS BELOW THIS LINE

-- Example Script 1, no delay
addScript(function()
print("Executing Script 1")
-- Your actual script code here
coroutine.yield() -- allow other scripts to run
end)

-- Example Script 2, 1 second delay
addScript(function()
print("Executing Script 2")
-- Your actual script code here
coroutine.yield() -- allow other scripts to run
end, 1)

-- Example Script 3, 2 second delay
addScript(function()
print("Executing Script 3")
-- Your actual script code here
coroutine.yield() -- allow other scripts to run
end, 2)

-- Example Script 4, 3 second delay
addScript(function()
print("Executing Script 4")
-- Your actual script code here
coroutine.yield() -- allow other scripts to run
end, 3)

-- Example Script 5, 4 second delay
addScript(function()
print("Executing Script 5")
-- Your actual script code here
coroutine.yield() -- allow other scripts to run
end, 4)

-- YOUR SCRIPTS END HERE

-- Run all scripts
runAllScripts()
```

### how to add your scripts with delay

1. **find the section** labeled **"ADD YOUR SCRIPTS BELOW THIS LINE"**.
2. **add your scripts** using the `addScript` function with an optional delay in seconds.
### example to add a new script with a delay

simply add your script content and specify the delay time:

```lua
-- Script with a 5 second delay
addScript(function()
print("Executing My Delayed Script")
-- Your actual script code here
coroutine.yield() -- allow other scripts to run
end, 5)
```

### benefits

1. **minimalistic**: simple and easy to understand.
2. **concurrent execution**: allows multiple scripts to run concurrently.
3. **delayed execution**: provides control over when each script starts.
4. **executor compatibility**: designed for client-side execution in Roblox.

This template ensures that your scripts run efficiently and concurrently, with the added ability to specify delays in their execution.
