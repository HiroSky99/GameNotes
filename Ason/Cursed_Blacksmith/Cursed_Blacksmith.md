# Cursed_Blacksmith / 苍色之光与魔剑锻造师 v0.86e

## 第一步 解包 asar 文件，并让游戏读取解包后的文件夹启动

1- 使用 cmd 安装 Asar:

    CMD: npm install -g asar js-beautify
    如果出现 "npm" 不是内部或外部命令, 测试
    node -v
    npm -v

2- 在 cmd 中将当前目录导向游戏根目录中的 `resources` 文件夹

    CMD: X:
    CMD: cd X:\游戏根目录\resources

3- 将存放游戏资源的 `app.asar` 提取为一个名为 `app` 的文件夹 (要等一会):

    CMD: asar extract app.asar app

4- 重命名 `app.asar` 文件作为备份 (可以用 CMD-ren PowerShell-mv 或者直接重命名):

    (重命名后游戏引擎将读取 app 文件夹启动游戏而不是原先的 app.asar 文件)
    CMD: ren app.asar app.asar.bak

## 第二步 开始修改游戏

### _魔剑回旋斩_ 和 _魔剑强袭_ 降低侵蚀度而不是增加

1- 打开游戏目录下的以下文件 `resources\app\src\js\plugins\AS_EX.js`

2- 定位 `Dainsleif_erosion` 方法并修改

    battler.erosion += v
    改成
    battler.erosion -= v

### _魔剑武装_ 每回合降低侵蚀度而不是增加

1- 打开游戏目录下的以下文件 `resources\app\src\js\plugins\AS_GamePlayer.js`

2- 定位 `Game_Player.prototype.state_run_turns` 方法并修改

    battler.erosion += battler._erosionPlus
    改成
    battler.erosion -= battler._erosionPlus

    battler.erosion += 1
    改成
    battler.erosion -= 1

### 随着回合进行降低侵蚀度而不是增加

1- 打开游戏目录下的以下文件 `resources\app\src\js\plugins\AS_GameMap.js`

2- 定位 `Game_Map.prototype.updateTurnMove` 方法并修改

    battler.erosion++
    改成
    battler.erosion--

### 开局的初始负重值

1- 打开游戏目录下的以下文件 `resources\app\src\js\plugins\AS_EX.js`

2- 定位 `soulImprintClear` 方法并修改

    actor.weightMax = 25
    改成
    actor.weightMax = 1025

### 给 _恢復藥水_ 加上漂浮效果

1- 打开游戏目录下的以下文件 `resources\app\src\data\Items.json`

2- 定位 _恢復藥水_ 的数据并修改

    effects":[]
    改成
    effects":[{"code":21,"dataId":33,"value1":1,"value2":0}]

### 替换 _活力藥水_ 和 _天眼之石_ 的 id

1- 打开游戏目录下的以下文件 `resources\app\src\data\Items.json`

2- 替换 id-3- _活力藥水_ 和 id-38- _天眼之石_

### 修改 _魔劍迴旋斬_ 相对于 _詛咒深度_ 的伤害倍率

1- 打开游戏目录下的以下文件 `resources\app\src\data\Skills.json`

2- 找到 _魔劍迴旋斬_ 的位置并修改倍率从 2 到 20

    "name":"魔劍迴旋斬","note":"Fixed element\nTool Id : 15\ncostDurability : 0\nRD : 2\nKP : 2\nERC : 5"
    改成
    "name":"魔劍迴旋斬","note":"Fixed element\nTool Id : 15\ncostDurability : 0\nRD : 20\nKP : 2\nERC : 5"

### 修改 _魔劍強襲_ 的行动范围从 2 到 20

1- 打开游戏目录下的以下文件 `resources\app\src\data\Skills.json`

    name":"魔劍強襲","note":"Fixed element\nTool Id : 64\ncostDurability : 0\nRD : 1.8\nKP : 2\nJP : 2\nRG : 2\nERC : 0"
    改成
    name":"魔劍強襲","note":"Fixed element\nTool Id : 64\ncostDurability : 0\nRD : 1.8\nKP : 2\nJP : 2\nRG : 20\nERC : 0"
