-- Command prefix
local COMMAND_PREFIX = "!"

-- Admin commands
local function kickPlayer(player, target)
    target:Kick("You have been kicked by an admin.")
end

local function banPlayer(player, target)
    -- Add code to ban the player from the game
    -- Example: game.Players:FindFirstChild(target.Name):Kick("You have been banned by an admin.")
end

local function teleportPlayer(player, target)
    -- Add code to teleport the player to the admin
    -- Example: target.Character:SetPrimaryPartCFrame(player.Character.PrimaryPart.CFrame)
end

local function giveItem(player, target, item)
    -- Add code to give the player an item
    -- Example: game.ServerStorage[item]:Clone().Parent = target.Backpack
end

-- Chat command handler
local function onChat(message, player)
    local args = message:split(" ")
    local command = args[1]:lower()
    local targetName = args[2]
    local targetPlayer = game.Players:FindFirstChild(targetName)

    if command == COMMAND_PREFIX.."kick" then
        if targetPlayer then
            kickPlayer(player, targetPlayer)
        else
            player:Kick("Player not found.")
        end
    elseif command == COMMAND_PREFIX.."ban" then
        if targetPlayer then
            banPlayer(player, targetPlayer)
        else
            player:Kick("Player not found.")
        end
    elseif command == COMMAND_PREFIX.."teleport" then
        if targetPlayer then
            teleportPlayer(player, targetPlayer)
        else
            player:Kick("Player not found.")
        end
    elseif command == COMMAND_PREFIX.."giveitem" then
        local item = args[3]
        if targetPlayer and item then
            giveItem(player, targetPlayer, item)
        else
            player:Kick("Usage: !giveitem <player> <item>")
        end
    end
end

-- Connect chat event
game:GetService("Players").PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(message)
        onChat(message, player)
    end)
end)
 This script listens for chat messages from players and interprets them as admin commands.
The admin commands supported are: !kick, !ban, !teleport, and !giveitem.
Players must use the command prefix (! by default) followed by the command name and any additional arguments.
