import random
import sys

class BattleShipGame:
    def __init__(self):
        # 班級：二己 座號：27 姓名：柯鎮秦 (James)
        self.size = 10
        self.letters = "ABCDEFGHIJ"
        # 狀態：None(迷霧), 0(水花), 1(擊中), 2(擊沉), 3(玩家標記的空位 #)
        self.grid_data = {f"{l}{n}": None for l in self.letters for n in range(1, 11)}
        self.ships = []
        
        self.energy = 180 
        self.sunk_count = 0
        self.total_ships = 5
        self.turn = 1
        self._place_static_ships()

    def display(self):
        print("\n    " + " ".join([f" {l} " for l in self.letters]))
        for n in range(1, 11):
            row = f"{n:2d} "
            for l in self.letters:
                state = self.grid_data[f"{l}{n}"]
                if state is None:   icon = " . " 
                elif state == 0:    icon = " ~ " # 飛彈打過的空位
                elif state == 1:    icon = "[X]" # 擊中船段
                elif state == 2:    icon = "[#]" # 擊沉
                elif state == 3:    icon = " # " # 玩家標記的空位
                row += icon
            print(row)
        
        print("-" * 45)
        print(f"回合: {self.turn:02d} | 能量: {self.energy:3d} | 擊沉: {self.sunk_count}/{self.total_ships}")
        print("指令: 1.[飛彈](25) | 2.[核彈](75) | 3.[標記空位](5) | 0.[待命](+20)")
        print("-" * 45)

    def _place_static_ships(self):
        lengths = [5, 4, 3, 3, 2]
        self.all_ship_coords = set()
        for length in lengths:
            while True:
                d = random.choice(['H', 'V'])
                ls = random.randint(0, 9 - (length if d == 'H' else 0))
                ns = random.randint(1, 11 - (length if d == 'V' else 0))
                coords = [f"{self.letters[ls+i if d=='H' else ls]}{ns+i if d=='V' else ns}" for i in range(length)]
                if not any(c in self.all_ship_coords for c in coords):
                    self.ships.append({"coords": coords, "hits": 0, "sunk": False})
                    self.all_ship_coords.update(coords)
                    break

    def mark_empty(self, coord):
        """[新增機制] 標記空位，若重疊則遊戲結束"""
        if self.energy < 5: return print("❌ 能量連標記都不夠了！")
        if self.grid_data[coord] is not None: return print("❌ 該處已有記錄，無法標記。")
        
        self.energy -= 5
        # 判定是否與任何船隻座標重疊
        if coord in self.all_ship_coords:
            self.display()
            print(f"\n💥 【誤判引爆！】 座標 {coord} 其實有伏兵！")
            print("🚨 標記點與敵艦重疊，引發連鎖反應，任務失敗。")
            sys.exit() # 直接結束程式
        else:
            self.grid_data[coord] = 3
            print(f"📍 成功標記 {coord} 為安全區。")
        self.turn += 1

    def _apply_strike(self, coord):
        if self.grid_data[coord] in [1, 2]: return False
        hit_any = False
        for s in self.ships:
            if coord in s["coords"] and not s["sunk"]:
                s["hits"] += 1
                self.grid_data[coord] = 1
                hit_any = True
                if s["hits"] == len(s["coords"]):
                    s["sunk"] = True
                    self.sunk_count += 1
                    for c in s["coords"]: self.grid_data[c] = 2
                    self.energy += 30
                    print(f"🔥 敵艦擊沉！能量補給 +30")
                break
        if not hit_any: self.grid_data[coord] = 0
        return hit_any

    def fire_missile(self, coord):
        if self.energy < 25: return print("❌ 能量不足發射飛彈。")
        self.energy -= 25
        if self._apply_strike(coord): print(f"💥 命中 {coord}！")
        else: print(f"🌊 {coord} 是海域。")
        self.turn += 1

    def fire_nuke(self, coord):
        if self.energy < 75: return print("❌ 能量不足發射核彈。")
        self.energy -= 75
        l_idx, n_center = self.letters.find(coord[0]), int(coord[1:])
        print(f"🚀 核彈轟炸中...")
        for li in range(l_idx-1, l_idx+2):
            for ni in range(n_center-1, n_center+2):
                if 0 <= li < 10 and 1 <= ni <= 10:
                    self._apply_strike(f"{self.letters[li]}{ni}")
        self.turn += 1

    def play(self):
        print("\n" + "★"*20)
        print("🚢 資訊熵海戰：判官挑戰版")
        print("💡 警告：使用指令 3 標記空位，若標錯位置將直接戰敗！")
        print("★"*20)
        
        while self.sunk_count < self.total_ships:
            self.display()
            try:
                raw = input("指令 (例: 1 A1 / 3 B2 / 0): ").upper().split()
                if not raw: continue
                act = raw[0]
                if act == '0':
                    self.energy += 20; self.turn += 1; print("💤 回充能量..."); continue
                
                target = raw[1]
                if act == '1': self.fire_missile(target)
                elif act == '2': self.fire_nuke(target)
                elif act == '3': self.mark_empty(target)
                else: print("❌ 無效指令")
            except: print("❌ 格式錯誤 (範例: 3 C5)")
        
        print(f"\n🎉 完美大捷！James 指揮官展現了驚人的推理能力，耗時 {self.turn} 回合。")

if __name__ == "__main__":
    BattleShipGame().play()
