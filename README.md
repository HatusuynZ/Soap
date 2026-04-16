luau

# 🧼 Soap
A lightweight cleanup utility for Roblox/Luau. Soap keeps track of objects like Instances, connections, threads, tweens, and functions — and destroys them all at once when you're done.

# 🚀 Quick Start
```luau
lualocal soap = Soap.New()

local part = Instance.new("Part")
local connection = part.Touched:Connect(function() end)
local thread = task.delay(5, function() end)

soap:Add(part, connection, thread)

-- Later, when you're done:
soap:Cleanup()
```

# 🧪 Example
```luau
local Soap = require(path.to.Soap)

local function setup(part)
    local soap = Soap.New()

    soap:Add(
        part.Touched:Connect(function()
            print("Touched!")
        end),
        task.delay(10, function()
            print("10 seconds passed")
        end)
    )

    return soap
end
```

## 📖 Supported Types

| Type | Action |
|---|---|
| `Instance` | `:Destroy()` |
| `RBXScriptConnection` | `:Disconnect()` |
| `thread` | `task.cancel()` |
| `function` | called with no arguments |
| `Tween` | `:Cancel()` |
| `table` (nested) | recursively cleaned |

# 📝 Notes

Nested tables are supported: if you add a table, Soap will recursively clean its contents.
Cleanup() is safe to call multiple times — it won't error on an already-empty instance.
Destroy() should be called when the Soap instance itself is no longer needed.
