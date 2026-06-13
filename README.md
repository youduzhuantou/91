本地StarterGui=游戏：GetService("StarterGui")
本地玩家=游戏：GetService(“玩家”)
本地白名单玩家={
    ["9178883211111111"]=true，
    [""]=true，
    [""]=true，
    [""]=true，
}

本地函数IsWhitelisted(播放器)
返回白名单玩家[player.name]or false
结束

本地localPlayer=players.LocalPlayer

本地isLocalPlayerWhitelisted=IsWhitelisted(localPlayer)

如果isLocalPlayerWhitelisted，则
StarterGui:SetCore("SendNotification"，{
标题="白名单认证"，
文本="玩家："..localPlayer.Name.."，检测完毕白名单玩家，稍后会加载脚本"，
持续时间=7，
    })

    -- 加载UI主体功能
    本地NothingLibrary=loadstring(游戏：HttpGetAsync('https://raw.githubusercontent.com/3345-c-a-t-s-u-s/NOTHING/main/source.lua'))();
    本地Windows=NothingLibrary.new({
    title="by Vista"，
    说明="踢出一个幸运方块"，
    keybind=枚举.KeyCode.LeftControl，
    logo='http://www.roblox.com/asset/?id=18898582662'
    })

    本地TabFrame=Windows:Newtab({
    title="主要功能"，
    说明=""，
    icon="rbxassetid://7733960981"
    })

    本地节=TabFrame:NewSection({
    title="自动功能"，
    icon="rbxassetid://7743869054"，
    position="Left"
    })

    本地信息节=TabFrame:NewSection({
    title="信息"，
    icon="rbxassetid://7733964719"，
    position="Right"
    })

    本地kickLoop=false
    本地taviLoop=false
    local kickPower = 1.00

    Section:NewToggle({
        Title = "自动踢幸运方块",
        Default = false,
        Callback = function(state)
            kickLoop = state
            if kickLoop then
                task.spawn(function()
                    while kickLoop do
                        local args = {kickPower, 1}
                        game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("Packages"):WaitForChild("Network"):WaitForChild("rev_KickEvent"):FireServer(unpack(args))
                        task.wait()
                    end
                end)
            end
        end
    })

    Section:NewSlider({
        Title = "踢出力度",
        Min = 0.00,
        Max = 1.00,
        Default = 1.00,
        Decimal = 2,
        Step = 0.001,
        Callback = function(val)
            kickPower = math.floor(val * 100) / 100
        end
    })

    Section:NewToggle({
        Title = "叠加锻炼x2",
        Default = false,
        Callback = function(state)
            taviLoop = state
            if taviLoop then
                task.spawn(function()
                    while taviLoop do
                        game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("Packages"):WaitForChild("Network"):WaitForChild("rev_TaviMishkal"):FireServer()
                        task.wait()
                    end
                end)
            end
        end
    })

    Section:NewButton({
        Title = "出售手持",
        Callback = function()
            game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("Packages"):WaitForChild("Network"):WaitForChild("ref_B_Sell"):InvokeServer()
        end
    })

    Section:NewButton({
    标题="出售所有"，
    callback=函数()
    game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("Packages"):WaitForChild("Network"):WaitForChild("ref_B_SellAll"):InvokeServer()
    结束
    })

    节：NewButton({
    标题="一键拿下所有脑红"，
    callback=函数()
    对于num=1，30do
    本地参数={num}
    game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("Packages"):WaitForChild("Network"):WaitForChild("rev_S_Interact"):FireServer(unpack(args))
    结束
    结束
    })

其他
localPlayer：踢("你没有被加入白名单，请找群主反馈或购买")
结束
