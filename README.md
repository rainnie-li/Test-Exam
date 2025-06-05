# Test-Exam
### Java Journal Template

**Name:** [Your Name]  
**Date:** [Submission Date]  
**Final IDE Program Join Link:** [Insert Your IDE Share Link Here]

---

### PART 1: Defining Your Problem  
**Task:** State the problem you are planning to solve.  

**Problem Statement:**  
Develop a simulation program for the casino dice game Craps to help users understand betting odds and statistical outcomes.  

**Input Data:**  
- User input for number of games to simulate  
- Randomly generated dice rolls  

**Program Functionality:**  
1. Simulate a sample game to demonstrate gameplay  
2. Prompt user for number of games to play  
3. Execute multiple game simulations based on user input  
4. Track win/loss statistics and average rolls per outcome  

**Outputs/Results:**  
- Real-time display of each simulated game's outcome  
- Summary statistics including:  
  - Total games played  
  - Win percentage  
  - Average rolls per win/loss  
  - Timestamped log file with detailed results  

---

### PART 2: Working Through Specific Examples  
**Task:** Write down clear steps for simplified scenarios.  

**Scenario 1: Player wins on first roll**  
1. Roll two dice (values: 4 + 3 = 7)  
2. Check if sum equals 7 or 11 → Win  
3. Output: "Player wins in 1 roll"  

**Scenario 2: Player loses after multiple rolls**  
1. Initial roll: 2 + 5 = 7 → Win  
2. Subsequent game:  
   - Roll 1: 3 + 6 = 9 (point established)  
   - Roll 2: 4 + 2 = 6 → Continue  
   - Roll 3: 5 + 1 = 6 → Continue  
   - Roll 4: 6 + 0 = 6 → Continue  
   - Roll 5: 2 + 4 = 6 → Continue  
   - Roll 6: 3 + 3 = 6 → Continue  
   - Roll 7: 1 + 6 = 7 → Lose  

---

### PART 3: Generalizing Into Pseudocode  
**Task:** Outline program structure using pseudocode.  
// 1. 初始化游戏统计变量
SET totalGames = 0          // 总模拟局数
SET totalWins = 0           // 总胜利局数
SET totalLosses = 0         // 总失败局数
SET totalRolls = 0          // 总骰子滚动次数
SET logFile = "craps_log.txt"  // 结果日志文件路径

// 2. 运行演示游戏（固定初始种子便于复现）
DISPLAY "===== SAMPLE GAME DEMO ====="
SEED_RANDOM_GENERATOR(12345)  // 固定随机种子确保示例可重现
CALL PlayGame() → STORE gameResult, rolls
DISPLAY "Sample Game Result: " + gameResult
DISPLAY "Roll Details: " + rolls

// 3. 获取用户输入并验证
DISPLAY "Enter number of games to simulate (e.g., 1000):"
READ userInput
WHILE userInput IS NOT A VALID INTEGER
    DISPLAY "Invalid input. Please enter a whole number."
    READ userInput
END WHILE
SET numberOfGames = INTEGER(userInput)

// 4. 执行多局模拟
FOR EACH game IN 1..numberOfGames
    SEED_RANDOM_GENERATOR(NOW())  // 每局使用当前时间作为随机种子
    CALL PlayGame() → STORE gameResult, rolls, rollsCount
    IF gameResult == "WIN"
        INCREMENT totalWins
    ELSE
        INCREMENT totalLosses
    END IF
    ADD rollsCount TO totalRolls
END FOR

// 5. 计算统计数据
SET winPercentage = (totalWins / numberOfGames) * 100
SET averageRolls = totalRolls / numberOfGames

// 6. 格式化输出结果
DISPLAY "===== SIMULATION RESULTS ====="
DISPLAY "Total Games Played: " + numberOfGames
DISPLAY "Win Rate: " + winPercentage + "%"
DISPLAY "Average Rolls per Game: " + ROUND(averageRolls, 2)
DISPLAY "Detailed Log: " + logFile

// 7. 将结果写入日志文件
APPEND_TO_FILE(logFile, 
    "Simulation Run at: " + CURRENT_DATETIME() + "\n" +
    "Games: " + numberOfGames + "\n" +
    "Wins: " + totalWins + "\n" +
    "Losses: " + totalLosses + "\n" +
    "Average Rolls: " + ROUND(averageRolls, 2) + "\n\n"
)

// 8. 异常处理模块（独立伪代码段）
FUNCTION ValidateInput(input)
    IF input CONTAINS NON-NUMERIC CHARACTERS
        THROW InputFormatException
    ELSE IF input < 1
        THROW InvalidArgumentException
    END IF
END FUNCTION

// 9. 游戏逻辑核心函数（详细伪代码）
FUNCTION PlayGame()
    SET die1 = RANDOM(1, 6)
    SET die2 = RANDOM(1, 6)
    SET sum = die1 + die2
    SET rolls = [die1, die2]
    SET gameStatus = "ONGOING"

    IF sum IN [2, 3, 12]
        SET gameStatus = "LOSE"
    ELSE IF sum IN [7, 11]
        SET gameStatus = "WIN"
    ELSE
        SET point = sum
        REPEAT
            SET die1 = RANDOM(1, 6)
            SET die2 = RANDOM(1, 6)
            SET sum = die1 + die2
            APPEND sum TO rolls
---

### PART 4: Testing Your Program  
**Task:** Document testing process and error fixes.  

**Test Case 1:** Invalid user input (non-numeric value)  
- **Error:** `InputMismatchException`  
- **Fix:**  
  ```java
  try {
      numberOfGames = scanner.nextInt();
  } catch (InputMismatchException e) {
      System.out.println("Invalid input. Please enter a number.");
      scanner.nextLine(); // Clear buffer
  }// DiceRoll class represents a single dice roll
public class DiceRoll {
    private int die1; // Value of first die (1-6)
    private int die2; // Value of second die (1-6)
    
    // Constructor initializes random dice values
    public DiceRoll() {
        Random rand = new Random();
        die1 = rand.nextInt(6) + 1; // Generate 1-6
        die2 = rand.nextInt(6) + 1;
    }
    
    // Returns sum of both dice
    public int getSum() {
        return die1 + die2;
    }
}
            IF sum == 7
                SET gameStatus = "LOSE"
            ELSE IF sum == point
                SET gameStatus = "WIN"
            END IF
        UNTIL gameStatus != "ONGOING"
    END IF

    RETURN (gameStatus, rolls)
END FUNCTION
