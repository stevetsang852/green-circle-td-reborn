# Green Circle TD Reborn

Pixel-style 2D Web Tower Defense hybrid game.

**Inspired by:** Green Circle TD + Legion TD + Auto Battler  
**Style:** Pixel Art  
**Tech:** Phaser 3 + React + TypeScript (Client-first)  
**Future Backend:** Java Spring Boot + WebSocket + PostgreSQL + Redis

---

## 核心理念

Green Circle TD 成功的核心不是「迷宮建造」，而是：

- Build Optimization（建塔優化）
- 經濟管理
- 隨機性
- 多人合作
- 長時間成長感
- 高 Replayability

我們不做 100% Copy，而是保留核心精髓再簡化，適合 Web / 手機。

---

## 遊戲定位

**Green Circle TD + Legion TD + Auto Battler 混合版**

- 保留 Green TD 的建塔樂趣
- 先做多人組隊合作通關（最多 4 人）
- 可選 Auto Battler 模式（自動戰鬥）
- 適合瀏覽器、手機、Telegram Mini App
- **多人競技（PVP）先不做**

---

## MVP 範圍（最快 1-2 個月可玩）

### Phase 1 - 100% Client Side

**技術棧：**
- React
- TypeScript
- Phaser 3
- LocalStorage

**功能：**
- 單人
- 多人組隊合作（最多 4 人通關，Client Side 預留）
- 固定路線地圖（20×20 Grid 或蛇形路徑）
- 5 種基礎塔（Arrow / Fire / Ice / Poison / Tesla）
- 簡單合成系統
- 20 Waves
- 每 5 波 Roguelike Buff 選擇
- 本地存檔（Gold / XP / Unlock）
- 排行榜接口預留
- 多人接口預留（MockGameServer，支援合作房間）

**不做：**
- 不做完整迷宮建造（手機難玩）
- 不做真實後端（先做 Client Side）
- 不做多人競技 / PVP（先做合作通關）
- 不做 NFT / Web3（先 Free To Play）

---

## 技術架構（API 抽象）

```
src/
├─ api/
│  ├─ GameApi.ts
│  ├─ PlayerApi.ts
│  └─ RankingApi.ts
│
├─ services/
│  ├─ LocalGameApi.ts
│  └─ RemoteGameApi.ts
```

```typescript
export interface PlayerApi {
  loadPlayer(): Promise<Player>;
  savePlayer(player: Player): Promise<void>;
}

export class LocalPlayerApi implements PlayerApi {
  async loadPlayer() {
    return JSON.parse(localStorage.getItem("player") ?? "{}");
  }
  async savePlayer(player: Player) {
    localStorage.setItem("player", JSON.stringify(player));
  }
}
```

未來只要換成 `RemotePlayerApi` 即可，Game Logic 完全不使改。

---

## 地圖設計

**不照抄 Green TD 迷宮建造。**

改用**固定路線**：

```
入口
↓↓↓
→→→→↓
↑      ↓
↑      ↓
←←←←←
出口
```

玩家只需要放塔，開發速度快 10 倍，手機也好玩。

---

## 塔種類（MVP）

**基礎 5 種：**
- Arrow
- Fire
- Ice
- Poison
- Tesla

**合成例子（Element TD 風）：**
- Arrow + Fire = Flame Tower
- Fire + Water = Steam Tower
- Poison + Magic = Necro Tower

---

## Roguelike 元素（強烈推薦）

每 5 波選 1 個 Buff：

- +15% Attack
- +20% Crit
- Fire Tower +1 Bounce
- Boss HP +30%
- Gold +60%

大幅提升重玩價值，參考 Vampire Survivors / Brotato。

---

## 多人模式

### 組隊合作（優先做，Client Side 先實作）
- 最多 4 人合作通關
- 可分區域（例如左上 / 右上 / 左下 / 右下）
- 共享：血量、Buff、Boss、資源
- 目標：一起守城到最後
- 目前先用 MockGameServer 做本地模擬，之後再接 WebSocket

### PVP（先不做）
- 競技派兵機制（Legion TD 風）延後再考慮
- 目前專注合作通關體驗

---

## 未來 Server 架構

```
Client
  |
  |
REST / WebSocket
  |
Spring Boot
  |
Redis + PostgreSQL
```

---

## 資產（Pixel Style）

使用**免費、開放授權 / CC0 / Public Domain** 的 Pixel Art 資源。

推薦來源（均可商用，無版權問題）：

- **Kenney Tower Defense (Top-Down)** - CC0  
  https://opengameart.org/content/tower-defense-top-down

- **Kenney Tower Defense Kit** - CC0  
  https://opengameart.org/content/tower-defense-kit

- **CodeLaboratory - Pixel Tower Defenders Asset Pack** - Free to use (don't resell assets)  
  https://codelaboratory.itch.io/pixel-tower-defenders-asset-pack

- **finalbossblues - Pixel Shooter and Towers Asset Pack** - Public Domain  
  https://finalbossblues.itch.io/pixel-shooter-towers-asset-pack

- **Tiddybub/2d-assets** - Curated CC0 collection  
  https://github.com/Tiddybub/2d-assets

詳細資產下載與使用說明請見 `assets/README.md`。

---

## 開發優先順序

1. Phaser Scene 骨架 + 固定路線敵人移動
2. 塔放置 + 攻擊邏輯
3. 經濟系統 + 升級
4. Roguelike Buff 選擇畫面
5. LocalStorage 存檔 + API 抽象層
6. 多人合作 Mock 實作（Client Side）
7. 接 Spring Boot + WebSocket

---

## 目標

**Green Circle TD Reborn**

- Pixel 風格
- Single Player + 多人組隊合作（最多 4 人）
- Mobile Support
- 20 分鐘一局
- Roguelike Buff
- Leaderboard
- 先 Client Side，之後再接後端

技術棧完全符合現有 Frontend TypeScript + Backend Java 背景。

---

> 先做可玩的 Client 版（含合作預留），之後再接後端。  
> 不要一開始就做太完整，先驗證核心玩法與合作體驗。
