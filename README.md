# -*- coding: utf-8 -*-
# 《暗码追凶》交互式小说引擎核心逻辑

class StoryEngine:
    def __init__(self):
        # 初始化游戏状态
        self.clues = {
            "查看手机": False,
            "检查伤口": False,
            "铜戒刻字": False
        }
        self.current_chapter = 1
        self.endings_unlocked = []

    def show_chapter(self, chapter_num):
        # 这里加载章节内容（示例简化版）
        chapters = {
            1: {
                "text": "第一章 诺基亚的诅咒\n你站在图书馆的血案现场...",
                "choices": ["查看手机", "检查伤口", "离开现场"]
            },
            5: {
                "text": "第五章 审判倒计时\n卢卡斯在火光中举起手机...",
                "choices": ["夺走手机", "检查伤口", "转身离开"]
            }
        }
        return chapters.get(chapter_num, {"text": "章节不存在", "choices": []})

    def handle_choice(self, choice):
        # 记录关键线索
        if choice in self.clues:
            self.clues[choice] = True
            
        # 多结局路径判断
        if self.current_chapter == 5:
            if choice == "查看手机" or choice == "夺走手机":
                return self.ending_a()
            elif choice == "检查伤口":
                return self.ending_b()
            else:
                return self.ending_c()
        
        # 章节推进逻辑
        self.current_chapter += 1
        return self.show_chapter(self.current_chapter)

    def ending_a(self):
        self.endings_unlocked.append("A")
        return {
            "text": "结局A：赎罪直播\n火焰吞没实验室...",
            "achievement": "解锁真相结局"
        }

    def ending_b(self):
        self.endings_unlocked.append("B") 
        return {
            "text": "结局B：镜像罪孽\n新的文身刺痛皮肤...",
            "achievement": "解锁堕落结局"
        }

    def ending_c(self):
        self.endings_unlocked.append("C")
        return {
            "text": "结局C：集体沉默\n诺基亚在灰烬中响起...",
            "achievement": "解锁混沌结局"
        }

# ---------- 使用示例 ----------
if __name__ == "__main__":
    engine = StoryEngine()
    
    # 模拟玩家流程
    print("=== 第一章 ===")
    chapter = engine.show_chapter(1)
    print(chapter["text"])
    
    # 玩家选择查看手机
    result = engine.handle_choice("查看手机")
    print(f"\n=== {result['achievement']} ===")
    print(result["text"])
    
    # 查看解锁结局
    print(f"\n已解锁结局：{engine.endings_unlocked}")
